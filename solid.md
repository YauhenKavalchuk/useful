
## **SOLID**

### [YouTube: Просто о SOLID (Принципы ООП)](https://youtu.be/A6wEkG4B38E)
---

### Single responsibility principle

👎**Bad:**

```javascript
class Auto {
	constructor(model: string) { }
	getCarModel() { }
	saveCustomerOrder(o: Auto) { }
	setCarModel() { }
	getCustomerOrder(id: string) { }
	removeCustomerOrder(id: string) { }
	updateCarSet(set: object) { }
}
```

👍**Good:**
```javascript
class Auto {
	constructor(model: string) { }
	getCarModel() { }
	setCarModel() { }
}

class CustomerAuto {
	saveCustomerOrder(o: Auto) { }
	getCustomerOrder(id: string) { }
	removeCustomerOrder(id: string) { }
}

class AutoDB {
	updateCarSet(set: object) { }
}
```

### Open/closed principle

👎**Bad:**

```javascript
class Auto {
	constructor(public model: string) { }
	getCarModel() { }
}

const shop: Array<Auto> = [
	new Auto('Tesla'),
	new Auto('Audi'),
];

const getPrice = (auto: Array<Auto>): string | void => {
	for (let i = 0; i < auto.length; i++) {
		switch (auto[i].model) {
			case 'Tesla': return '80 000$';
			case 'Audi': return '50 000$';
			default: return 'No Auto Price';
		}
	}
}

getPrice(shop);
```

👍**Good:**
```javascript
abstract class CarPrice {
	abstract getPrice(): string;
}

class Tesla extends CarPrice {
	getPrice() {
		return '80 000$';
	}
}

class Audi extends CarPrice {
	getPrice() {
		return '50 000$';
	}
}

class Bmw extends CarPrice {
	getPrice() {
		return '70 000$';
	}
}

const shop: Array<CarPrice> = [
	new Tesla(),
	new Audi(),
	new Bmw(),
];

const getPrice = (auto: Array<CarPrice>): string | void => {
	for (let i = 0; i < auto.length; i++) {
		auto[i].getPrice();
	}
}

getPrice(shop);
```

### Liskov substitution principle

👎**Bad:**

```javascript
class Rectangle {
	constructor(public width: number, public height: number) {}

	setWidth(width: number) {
		this.width = width;
	}

	setHeight(height: number) {
		this.height = height;
	}

	areaOf(): number {
		return this.width * this.height;
	}
}

class Square extends Rectangle {
	width: number = 0;
	height: number = 0;

	constructor(size: number) {
		super(size, size);
	}

	setWidth(width: number) {
		this.width = width;
		this.height = width;
	}

	setHeight(height: number) {
		this.width = height;
		this.height = height;
	}
}
```

👍**Good:**
```javascript
interface Figure {
	setWidth(width: number): void;
	setHeight(height: number): void;
	areaOf(): void;
}

class Rectangle implements Figure {
	setWidth(width: number) { }
	setHeight(height: number) { }
	areaOf() { }
}

class Square implements Figure {
	setWidth(width: number) { }
	setHeight(height: number) { }
	areaOf() { }
}
```

### Interface segregation principle

👎**Bad:**

```javascript
interface AutoSet {
	getTeslaSet(): any;
	getAudiSet(): any;
	getBmwSet(): any;
}

class Tesla implements AutoSet {
	getTeslaSet(): any { };
	getAudiSet(): any { };
	getBmwSet(): any { };
}

class Audi implements AutoSet {
	getTeslaSet(): any { };
	getAudiSet(): any { };
	getBmwSet(): any { };
}

class Bmw implements AutoSet {
	getTeslaSet(): any { };
	getAudiSet(): any { };
	getBmwSet(): any { };
}
```

👍**Good:**
```javascript
interface TeslaSet {
	getTeslaSet(): any;
}

interface AudiSet {
	getAudiSet(): any;
}

interface BmwSet {
	getBmwSet(): any;
}

class Tesla implements TeslaSet {
	getTeslaSet(): any { };
}

class Audi implements AudiSet {
	getAudiSet(): any { };
}

class Bmw implements BmwSet {
	getBmwSet(): any { };
}
```

### Dependency inversion principle

👎**Bad:**

```javascript
class xmlHttpRequestService { }

// Low level
class xmlHttpService extends xmlHttpRequestService {
	request(url: string, type: string) { }
}

// High level module
class Http {
	constructor(private xmlHttpService: xmlHttpService) { }

	get(url: string, options: any) {
		this.xmlHttpService.request(url, 'GET');
	}

	post(url: string) {
		this.xmlHttpService.request(url, 'POST');
	}
}
```

👍**Good:**
```javascript
class xmlHttpRequestService {
	open() { }
	send() { }
}

interface Connection {
	request(url: string, options: any): any;
}

// Low level
class xmlHttpService implements Connection {
	xhr = new xmlHttpRequestService();

	request(url: string, type: string) {
		this.xhr.open();
		this.xhr.send();
	}
}

// High level module
class Http {
	constructor(private httpConnection: Connection) { }
	
	get(url: string, options: any) {
		this.httpConnection.request(url, 'GET');
	}

	post(url: string) {
		this.httpConnection.request(url, 'POST');
	}
}
```
