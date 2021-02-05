## **Clean Code**

### [YouTube: Просто о Чистом коде и качестве кода (Code Quality & Clean Code)](https://youtu.be/XT6XkIJIVbA)
---

## **Переменные**

### Используйте значимые и смысловые имена

👎**Bad:**
```javascript
const yyyymmdstr = moment().format('YYYY/MM/DD');
```

👍**Good:**
```javascript
const currentDate = moment().format('YYYY/MM/DD');
```

---
### Используйте один и тот же метод для одинаковых типов переменных

👎**Bad:**
```javascript
getUserInfo();
getClientData();
getCustomerRecord();
```

👍**Good:**
```javascript
getUser();
```

---
### Используйте именованные значения

👎**Bad:**
```javascript
// What the heck is 86400000 for?
setTimeout(blastOff, 86400000);
```

👍**Good:**
```javascript
// Declare them as capitalized named constants.
const MILLISECONDS_IN_A_DAY = 86400000;

setTimeout(blastOff, MILLISECONDS_IN_A_DAY);
```

---
### Используйте поясняющие переменные

👎**Bad:**
```javascript
const address = 'One Infinite Loop, Cupertino 95014';
const cityZipCodeRegex = /^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/;
saveCityZipCode(address.match(cityZipCodeRegex)[1], address.match(cityZipCodeRegex)[2]);
```

👍**Good:**
```javascript
const address = 'One Infinite Loop, Cupertino 95014';
const cityZipCodeRegex = /^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/;
const [_, city, zipCode] = address.match(cityZipCodeRegex) || [];
saveCityZipCode(city, zipCode);
```

---
### Избегайте интуитивных маппингов

👎**Bad:**
```javascript
const locations = ["Austin", "New York", "San Francisco"];
locations.forEach(l => {
	doSomething(l);
});
```

👍**Good:**
```javascript
const locations = ['Austin', 'New York', 'San Francisco'];
locations.forEach(location => {
	doSomething(location);
});
```

---
### Не добавляйте ненужный контекст

👎**Bad:**
```javascript
const Car = {
  carMake: 'Honda',
  carModel: 'Accord',
  carColor: 'Blue'
};

function paintCar(car) {
  car.carColor = 'Red';
}
```

👍**Good:**
```javascript
const Car = {
  make: 'Honda',
  model: 'Accord',
  color: 'Blue'
};

function paintCar(car) {
  car.color = 'Red';
}
```

---
### Используйте условия по умолчанию вместо коротких замыканий или условных выражений

👎**Bad:**
```javascript
const createFullName = (firstName, lastName) => {
	const fName = firstName || "Yauhen";
	// ...
}
```

👍**Good:**
```javascript
const createFullName = (firstName = "Yauhen", lastName = "Kavalchuk") => {
	// ...
}
```

## **Функции**

### Функция должна решать только одну задачу

👎**Bad:**
```javascript
const emailClients = (clients) => {
	clients.forEach(client => {
		const clientRecord = database.lookup(client);
		if (clientRecord.isActive()) {
			email(client);
		}
	});
}
```

👍**Good:**
```javascript
const emailActiveClients = (clients) => {
	clients.filter(isActiveClient).forEach(email);
}

const isActiveClient = (client) => {
	const clientRecord = database.lookup(client);
	return clientRecord.isActive();
}
```

---
### Имена должны описывать что функция делает

👎**Bad:**
```javascript
function addToDate(date, month) {
  // ...
}

const date = new Date();
// It's hard to to tell from the function name what is added
addToDate(date, 1);
```

👍**Good:**
```javascript
function addMonthToDate(month, date) {
  // ...
}

const date = new Date();
addMonthToDate(1, date);
```

---
### Не используйте флаги, как аргументы функций

👎**Bad:**
```javascript
const createFile = (name, temp) => {
	temp ? fs.create(`./temp/${name}`) : fs.create(name);
}
```

👍**Good:**
```javascript
const createFile = (name) => {
	fs.create(name);
}

const createTempFile = (name) => {
	createFile(`./temp/${name}`);
}
```

---
### Инкапсулируйте условия

👎**Bad:**
```javascript
if (fsm.state === "fetching" && isEmpty(listNode)) {
  // ...
}
```

👍**Good:**
```javascript
function shouldShowSpinner(fsm, listNode) {
  return fsm.state === "fetching" && isEmpty(listNode);
}

if (shouldShowSpinner(fsmInstance, listNodeInstance)) {
  // ...
}
```

---
### Избегайте негативных условий

👎**Bad:**
```javascript
function isDOMNodeNotPresent(node) {
  // ...
}

if (!isDOMNodeNotPresent(node)) {
  // ...
}
```

👍**Good:**
```javascript
function isDOMNodePresent(node) {
  // ...
}

if (isDOMNodePresent(node)) {
  // ...
}
```

---
### Идеальное количество аргументов для функций два и меньше

👎**Bad:**
```javascript
function createMenu(title, body, buttonText, cancellable) {
  // ...
}
```

👍**Good:**
```javascript
function createMenu({ title, body, buttonText, cancellable }) {
  // ...
}

createMenu({
  title: 'Foo',
  body: 'Bar',
  buttonText: 'Baz',
  cancellable: true
});
```

---
### Не переопределяйте глобальные функции

👎**Bad:**
```javascript
Array.prototype.diff = function diff(comparisonArray) {
  const hash = new Set(comparisonArray);
  return this.filter(elem => !hash.has(elem));
};
```

👍**Good:**
```javascript
class SuperArray extends Array {
  diff(comparisonArray) {
    const hash = new Set(comparisonArray);
    return this.filter(elem => !hash.has(elem));
  }
}
```

---
### Удаляйте мёртвый код

👎**Bad:**
```javascript
// Bad
function oldRequestModule(url) {
	// ...
}

function newRequestModule(url) {
	// ...
}

const req = newRequestModule;
inventoryTracker('apples', req, 'test-url');
```

👍**Good:**
```javascript
function newRequestModule(url) {
	// ...
}

const req = newRequestModule;
inventoryTracker('apples', req, 'test-url');
```

## Объекты
### Используйте приватные свойства

👎**Bad:**
```javascript
const Employee = function(name) {
  this.name = name;
};

Employee.prototype.getName = function getName() {
  return this.name;
};

const employee = new Employee('John Doe');
console.log(`Employee name: ${employee.getName()}`); // Employee name: John Doe
delete employee.name;
console.log(`Employee name: ${employee.getName()}`); // Employee name: undefined
```

👍**Good:**
```javascript
const Employee = function (name) {
  this.getName = function getName() {
    return name;
  };
};

const employee = new Employee('John Doe');
console.log(`Employee name: ${employee.getName()}`); // Employee name: John Doe
delete employee.name;
console.log(`Employee name: ${employee.getName()}`); // Employee name: John Doe
```

---
### Используйте геттеры и сеттеры

👎**Bad:**
```javascript
class BankAccount {
  constructor() {
    this.balance = 1000;
  }
}

const bankAccount = new BankAccount();
bankAccount.balance -= 100;
```

👍**Good:**
```javascript
class BankAccount {
  constructor(balance = 1000) {
    this._balance = balance;
  }

  set balance(amount) {
    if (this.verifyIfAmountCanBeSetted(amount)) {
      this._balance = amount;
    }
  }

  get balance() {
    return this._balance;
  }

  verifyIfAmountCanBeSetted(val) {
    // ...
  }
}

const bankAccount = new BankAccount();
bankAccount.balance -= shoesPrice;
let balance = bankAccount.balance;
```

## **Классы**

### Активно используйте принцип SOLID
- Принцип единственной ответственности 
- Принцип открытости/закрытости
- Принцип подстановки Барбары Лисков
- Принцип разделения интерфейса
- И принцип инверсии зависимостей

[Подробнее о принципе](https://github.com/YauhenKavalchuk/prosto-o/blob/master/01_solid.md)

---
### Используйте метод цепочки

👎**Bad:**
```javascript
class CarBuilder {

	constructor() {
		this.car = new Car();
	}

	addAutoPilot(autoPilot) {
		this.car.autoPilot = autoPilot;
	}

	addParktronic(parktronic) {
		this.car.parktronic = parktronic;
	}

	addSignaling(signaling) {
		this.car.signaling = signaling;
	}

	updateEngine(engine) {
		this.car.engine = engine;
	}

	build() {
		return this.car;
	}
}

const car = new CarBuilder();
car.addAutoPilot(true)
car.addParktronic(true)
car.updateEngine('V8')
car.build();
```

👍**Good:**
```javascript
class CarBuilder {

	constructor() {
		this.car = new Car();
	}

	addAutoPilot(autoPilot) {
		this.car.autoPilot = autoPilot;
		return this;
	}

	addParktronic(parktronic) {
		this.car.parktronic = parktronic;
		return this;
	}

	addSignaling(signaling) {
		this.car.signaling = signaling;
		return this;
	}

	updateEngine(engine) {
		this.car.engine = engine;
		return this;
	}

	build() {
		return this.car;
	}
}

const car = new Car()
	.addAutoPilot(true)
	.addParktronic(true)
	.updateEngine('V8')
	.build();
```

## **Тестирование**

### Один тест - одно описание

👎**Bad:**
```javascript
const assert = require('assert');

describe('MakeMomentJSGreatAgain', () => {
  it('handles date boundaries', () => {
    let date;

    date = new MakeMomentJSGreatAgain('1/1/2015');
    date.addDays(30);
    date.shouldEqual('1/31/2015');

    date = new MakeMomentJSGreatAgain('2/1/2016');
    date.addDays(28);
    assert.equal('02/29/2016', date);

    date = new MakeMomentJSGreatAgain('2/1/2015');
    date.addDays(28);
    assert.equal('03/01/2015', date);
  });
});
```

👍**Good:**
```javascript
const assert = require('assert');

describe('MakeMomentJSGreatAgain', () => {
  it('handles 30-day months', () => {
    const date = new MakeMomentJSGreatAgain('1/1/2015');
    date.addDays(30);
    date.shouldEqual('1/31/2015');
  });

  it('handles leap year', () => {
    const date = new MakeMomentJSGreatAgain('2/1/2016');
    date.addDays(28);
    assert.equal('02/29/2016', date);
  });

  it('handles non-leap year', () => {
    const date = new MakeMomentJSGreatAgain('2/1/2015');
    date.addDays(28);
    assert.equal('03/01/2015', date);
  });
});
```

## **Асинхронность**
### Используйте промисы вместо колбеков

👎**Bad:**
```javascript
request.get(url, (requestErr, response) => {
	requestErr ?
		console.error(requestErr) :
		fs.writeFile('article.html', response.body, (writeErr) => {
			writeErr ? console.error(writeErr): console.log('File written');
		});
});
```

👍**Good:**
```javascript
requestPromise.get(url)
	.then((response) => fsPromise.writeFile('article.html', response))
	.then(() => { console.log('File written'); })
	.catch((err) => { console.error(err); });
```

---
### Async/Await делает код чище, чем промисы

👎**Bad:**
```javascript
requestPromise.get(url)
	.then((response) => fsPromise.writeFile('article.html', response))
	.then(() => { console.log('File written'); })
	.catch((err) => { console.error(err); });
```

👍**Good:**
```javascript
async function getCleanCodeArticle(url) {
	try {
		const response = await requestPromise.get(url);
		await fsPromise.writeFile('article.html', response);
		console.log('File written');
	} catch(err) {
		console.error(err);
	}
}
```

---
### Не игнорируйте отловленные ошибки

👎**Bad:**
```javascript
try {
  functionThatMightThrow();
} catch (error) {
  console.log(error);
}
```

👍**Good:**
```javascript
try {
	functionThatMightThrow();
} catch (error) {
	console.error(error);
	notifyUserOfError(error);
	reportErrorToService(error);
}
```

## **Форматирование**
### Используйте один вариант именования

👎**Bad:**
```javascript
const DAYS_IN_WEEK = 7;
const daysInMonth = 30;

const songs = ['Back In Black', 'Stairway to Heaven', 'Hey Jude'];
const Artists = ['ACDC', 'Led Zeppelin', 'The Beatles'];

function eraseDatabase() {}
function restore_database() {}

class animal {}
class Alpaca {}
```

👍**Good:**
```javascript
const DAYS_IN_WEEK = 7;
const DAYS_IN_MONTH = 30;

const songs = ['Back In Black', 'Stairway to Heaven', 'Hey Jude'];
const artists = ['ACDC', 'Led Zeppelin', 'The Beatles'];

function eraseDatabase() {}
function restoreDatabase() {}

class Animal {}
class Alpaca {}
```

---
### Коментируйте только код, содержащий сложную бизнес-логику

👎**Bad:**
```javascript
function hashIt(data) {
  // The hash
  let hash = 0;

  // Length of string
  const length = data.length;

  // Loop through every character in data
  for (let i = 0; i < length; i++) {
    // Get character code.
    const char = data.charCodeAt(i);
    // Make the hash
    hash = ((hash << 5) - hash) + char;
    // Convert to 32-bit integer
    hash &= hash;
  }
}
```

👍**Good:**
```javascript
function hashIt(data) {
  let hash = 0;
  const length = data.length;

  for (let i = 0; i < length; i++) {
    const char = data.charCodeAt(i);
    hash = ((hash << 5) - hash) + char;

    // Convert to 32-bit integer
    hash &= hash;
  }
}
```

---
### Не комментируйте ненужный код

👎**Bad:**
```javascript
doStuff();
// doOtherStuff();
// doSomeMoreStuff();
// doSoMuchStuff();
```

👍**Good:**
```javascript
doStuff();
```

---
### Никогда не ведите журнал комментариев

👎**Bad:**
```javascript
/**
 * 2016-12-20: Removed monads, didn't understand them (RM)
 * 2016-10-01: Improved using special monads (JP)
 * 2016-02-03: Removed type-checking (LI)
 * 2015-03-14: Added combine with type-checking (JR)
 */
function combine(a, b) {
  return a + b;
}
```

👍**Good:**
```javascript
function combine(a, b) {
  return a + b;
}
```

---
### Не используйте позиционные маркеры

👎**Bad:**
```javascript
////////////////////////////////////////////////////////////////////////////////
// Scope Model Instantiation
////////////////////////////////////////////////////////////////////////////////
$scope.model = {
  menu: 'foo',
  nav: 'bar'
};

////////////////////////////////////////////////////////////////////////////////
// Action setup
////////////////////////////////////////////////////////////////////////////////
const actions = function() {
  // ...
};
```

👍**Good:**
```javascript
$scope.model = {
  menu: 'foo',
  nav: 'bar'
};

const actions = function() {
  // ...
};
```
