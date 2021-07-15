## **Практические задачи с собеседований**

### [YouTube: Front-end. Вопросы на собеседовании](https://www.youtube.com/playlist?list=PLNkWIWHIRwMFSLI9wBuHxuGI5lAZ7QNUg)
---

### Функция проверки палиндрома:
```javascript
// Base
function isPalindrome(str) {
  var arr = str.split('');
  var reverseArr = arr.reverse();
  var resString = reverseArr.join('');
  var res = str === resString;
  return res;
}

// Advanced
function isPalindrome(str) {
  return str === str.split('').reverse().join('');
}

// ES6
const isPalindrome = str =>
  str === str.split('').reverse().join('');
  
// Result:
isPalindrome('тест');     // false 
isPalindrome('шалаш');    // true  
```
---
### Функция поиска самого короткого слова:
```javascript
// Base
function findShort(string) {
  var wordsArr = string.split(' ');
  var sortedWordsArr = wordsArr.sort(function(a, b) {
    return a.length - b.length;
  });
  return sortedWordsArr[0];
}

// Advanced
function findShort(string) {
  return string
    .split(' ')
    .sort(function(a, b) { return a.length - b.length; })[0];
}

// ES6
const findShort = string =>
  string
    .split(' ')
    .sort((a, b) => a.length - b.length)[0];
    
// Resut:
findShort('The Smallest word in sentence');    // 'in'
findShort('Just test string');                 // 'Just'    
```
---
### Функция создания инициалов:
```javascript
// Base
function toInitials(name) {
  var nameArr = name.split(' ');
  var firsLettersArr = nameArr.map(function(el) {
    return el.slice(0,1).toUpperCase() + '.';
  });
  var initials = firsLettersArr.join('');
  return initials;
}

// Advanced
function toInitials(name) {
  return name
    .split(' ')
    .map(function(el) {
      return el.slice(0,1).toUpperCase() + '.';
    })
    .join('');
}

// ES6
const toInitials = name =>
  name
    .split(' ')
    .map(el => `${el.slice(0,1).toUpperCase()}.`)
    .join('');

// Result:
toInitials(‘Bill Gates’);    // 'B.G.'
toInitials(‘elon mask’);     // 'E.M.'
```
---
### Функция суммирования всех цифр числа:
```javascript
// Base
function sumDigits(number) {
  var moduleNumber = Math.abs(number);
  var str = moduleNumber.toString();
  var arr = str.split('');
  var res = arr.reduce(function(sum, cur) {
    return Number(sum) + Number(cur);
  }, 0);
  return res;
}

// Advanced
function sumDigits(number) {
  return Math.abs(number)
          .toString()
          .split('')
          .reduce(function(sum, cur) { return +sum + +cur }, 0);
}

// ES6
const sumDigits = number =>
  Math.abs(number)
    .toString()
    .split('')
    .reduce((sum, cur) => +sum + +cur, 0);

// Result:
sumDigits(99);     // 18
sumDigits(-32);    // 5
```
---
### Функция поиска минимального и максимального значений в массиве:
```javascript
// Base
function minMax(arr){
  var res = [];
  var minValue = Math.min.apply(null, arr);
  var maxValue = Math.max.apply(null, arr);
  return res.push(minValue, maxValue);
}

// Advanced
function minMax(arr){
  return [Math.min.apply(null, arr), Math.max.apply(null, arr)];
}

// ES6
const minMax = (arr) => 
  [Math.min(...arr), Math.max(...arr)];

// Result:
minMax([2, 9, 10, 25, 47, 4, 1]);  // [7, 47]
minMax([2, 1]);                    // [1, 2]
minMax([1]);                       // [1, 1]
```
---
### Функция создания набора дубликатов символов строки:
```javascript
// Base
function accum(string) {
  var arr = string.toUpperCase().split('');
  var repeatArr = arr.map(function(el,i) {
    return el += el.repeat(i).toLowerCase();
  });
  var resString = repeatArr.join('-');
  return resString;
}

// Advanced
function accum(string) {
 return string.toUpperCase().split('').map(
   function(el,i) {
     return el += el.repeat(i).toLowerCase();
   }
 ).join('-');
}

// ES6
const accum = (string) =>
  string
  .toUpperCase()
  .split('')
  .map((el,i) => `${el}${el.repeat(i).toLowerCase()}`).join('-');

// Result:
accum("abcd")   // "A-Bb-Ccc-Dddd"
accum("cwAt")   // "C-Ww-Aaa-Tttt"
```
---
### Функция возврата индексов заглавных букв строки:
```javascript
// Base
function capitals(word) {
  var bigLetters = word.toUpperCase().split('');
  var smallLetters = word.split('');
  var res = [];
  for(var i = 0; i < word.length; i++){
    if(smallLetters[i] === bigLetters[i]){
      res.push(i);
    }
  }
  return res;
};

// Advanced
function capitals(word) {
  var res = [];
  word.split('').forEach(function(letter, index) {
    if (letter === letter.toUpperCase()) {
      res.push(index);
    }
  });
  return res;  
};

// ES6:
const capitals = (word) =>
  word.split('').reduce((result, letter, index) => {
    if (letter === letter.toUpperCase()) {
      result.push(index);
    }
    return result;
  }, []);

// Result:
capitals('CodEWaRs');     // [0, 3, 4, 6] 
capitals('justForTest');  // [4, 7]
```
---
### Функция вывода чисел от 1 до n (n - передаваемый аргумент):
### Дополнительные условия:
- выводить `foo` вместо чисел, кратных 3;
- выводить `bar` вместо чисел, кратных 5;
- выводить `foobar` вместо чисел, кратных и 3, и 5.
```javascript
// Base
const fooBar = num => {
  for(let i = 1; i <= num; i++) {
    if (i % 3 === 0 && i % 5 === 0) {
      // multiple of 3 and 5
      console.log('foobar');
    } else if (i % 3 === 0) {
      // multiple of 3
      console.log('foo');
    } else if (i % 5 === 0) {
      // multiple 5
      console.log('bar');
    } else {
      // other numbers
      console.log(i);
    }
  }
};
```
---
### Функция возврата уникальных значений из нескольких массивов:
```javascript
// Base
function uniteUnique() {
  const arr = [...arguments];
  let newArr = [];
  for(var i = 0; i < arr.length; i++){
    newArr.push(...arr[i]); 
  }
  newArr = new Set(newArr);
  return [...newArr];
}

// Advanced
function uniteUnique() {
  return [...new Set([...arguments].flat())];
}

// Result:
uniteUnique([1,2,3], [4,1,5], [6,7,8,5]);     // [1, 2, 3, 4, 5, 6, 7, 8]
uniteUnique([1], [2], [3,2,2], [4,1,1,2]);    // [1, 2, 3, 4]
```
---
### Функция форматирования цифр в телефонный номер:
```javascript
// Base
function createPhoneNumber(number) {
  let numArr = number.toString().split('');
  numArr.splice(0,0,'(');
  numArr.splice(4,0,')');
  numArr.splice(5,0,' ');
  numArr.splice(9,0,'-');
  return numArr.join('');
}

// Advanced
const createPhoneNumber = (number) => {
  const strNum = number.toString();
  // template pattern: (xxx) xxx-xxx
  return `(${strNum.slice(0, 3)}) ${strNum.slice(3, 6)}-${strNum.slice(6, 9)}`;
}

// Result:
createPhoneNumber(123456789);        // "(123) 456-789"
createPhoneNumber(555095611);        // "(555) 095-611"
```
---
### Функция поиска гласных букв в строке:
```javascript
// Base
const findVowels = (str) => {
const vowels = ['a', 'e', 'i', 'o', 'u'];
  let count = 0;
  for(let char of str.toLowerCase()) {
    if(vowels.includes(char)) {
      count++;
    }
  }
  return count;
}

// Advanced
const findVowels = (str) => {
  const matches = str.match(/[aeiou]/gi);
  return matches ? matches.length : 0;
}

// Result:
findVowels('hello');					// 2
findVowels('hello world');		// 3
```
---
