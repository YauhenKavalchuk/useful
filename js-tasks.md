## **Практические задачи с собеседований**

### [YouTube: Front-end. Вопросы на собеседовании](https://www.youtube.com/playlist?list=PLNkWIWHIRwMFSLI9wBuHxuGI5lAZ7QNUg)
---

### Функция проверки палиндрома:
```javascript
// Base:
function isPalindrome(str) {
  var arr = str.split('');
  var reverseArr = arr.reverse();
  var resString = reverseArr.join('');
  var res = str === resString;
  return res;
}

// Advanced:
function isPalindrome(str) {
  return str === str.split('').reverse().join('');
}

// ES6:
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
