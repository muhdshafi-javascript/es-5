# ES-5
## Javascript Basics
### Variable and Data types
Javascript support dynamic typing, it auatomatically figure out the type.
1. **Number**: Floating point number
2. **String**: seaquence of chars (var x = 1+2+'3'+4; until a string found in left to right scan, consider it as a number)
3. **Boolean**: true or false (True and TRUE are invalid)
4. **Undefined**: varaible that doesn't have any value yet 
5. **Null**: non-existence (NULL and Null are invalid)
### Variable Mutation and Type Coercion
**Type coercion** is the process of converting value from one type to another (such as string to number, object to boolean, and so on).
```javascript
var name = 'Shafi';
var age = 31;
console.log(name + ' ' + age);//here age is converted to a String
//another example
var age = 31;
console.log(age == '31');//true
console.log(age === '31');//false
```
Re-assigning the value to variable is called **Variable Mutation**, javaScript dynamically change type based on the new value assigned.
```javascript
var age = 31;
console.log(typeof age, age);//number
 age = '31';
console.log(typeof age, age);//string
```
### Truthy and Falsy 
Falsy vakues are as given below 
1. **false**: boolean false
2. **0**: number 0
3. **'', "", ``**: Empty string
4. **null**: non existence
5. **undefined**: unassigned but variable is declared.
6. **NaN**: not a number
## Function Statements and Function Expressions
Globally in javascript statements doesn't return anything but an expression return a value.
examples for expression are 
1. invoke a function
2. execute 2+3 in console which gives the sum
examples of statements are
1. if(true){} in console

```javascript
//funtion statement
function funcStmt(){}
//funtion expression
var funcExpn = function(){}
```

## Arrays
```javascript
//a single array can hold values of different data types. 
var arr = [true, 31, '31', undefined, null];
console.log(arr);

//Print array elements
console.log(arr.toString());
//note that undefined and null didn't print

//add value to the end of the array
arr.push('shafi');
console.log(arr);

//add value to the begining of the array
arr.unshift('Muhd');
console.log(arr);

//remove element from the end
arr.pop();
console.log(arr);

//remove element from the begining
arr.shift();arr.shift();arr.shift();
console.log(arr);

//check if an element present or find the index
//Type coercion is not applied here.
console.log(arr.indexOf(31));
console.log(arr.indexOf('31'));
```
## Loops
1. Traditional for, while, do...while
   - you can use **continue** and **break** 
2. for...in
   - iterate over the keys of an object
```javascript
var string1 = "";
var object1 = {a: 1, b: 2, c: 3};

for (var property1 in object1) {
  string1 += object1[property1];
}

console.log(string1);
// expected output: "123"
```
- for...in consider enumerable the properties from prototype as well.
- Object.keys() and Object.getOwnPropertyNames() consider only the own properties

## How JavaScript works behind the scene
- Javascript engine execute the code(eg:V8)
  - Parseed by a Parser (check syntax, if everything is fine it produces a data struxture known as Abstract Syntax Tree)
  - Then Convert it to Machine code
  - Code runs  
### Execution Context and Execution Stack
- **Execution context** is container which stores variables and in which a piece of our code is evaluated and executed.
- **Global Execution Context** is default context where the code placed outside any function is executed(window object in browser).
- when function is invoked a new execution context is added on top of the global execution context, when another funtion is invoked from the 1st funtion another execution context is added on top of the existing one and so on. When a funtion execution is done the curresponding execution context is removed from the stack.
- **Execution stack** also known as “calling stack”, is a stack with a LIFO structure, which is used to store all the execution context created during the code execution.
- Execution context has 3 properties
  - Variable Objects ( contains funtion argumnets, local variables and function declartion)
  - Scope chain (VO and VO of parent)
  - *this* variable
- Phases of Execution context  
  - Creation phase
    - creation of VO
    - Creation of Scope chain
    - Determine the value of *this*
  - Execution phase
    The code of the funtion that generated the execution context run line by line.
  
