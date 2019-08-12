# ES-5 
A short note for self learing purpose.
## Javascript Basics
### Variable and Data types
Javascript support dynamic typing, it automatically figure out the type.
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
Globally in javascript, statements doesn't return anything but an expression return a value.

Examples for expression are 
 1. invoke a function
 2. execute 2+3 in console which gives the sum.
 
Examples of statements are
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
  - **Creation phase**
    - creation of VO
      - The argument object is created which contains all the args passed.
      - Code is scanned for **funtion declarations**, for each function, a property is created in the Variable object and point it to the funtion.
      - Code is scanned for **Variable declarations**, for each varible, a property is created in the VO and set to "undefined"
      - The 2nd and 3rd points together is called as **Hoisting**, in practice, we can invoke funtion which is declared below in the code and still it works, it is possible beacuse all the varibales and functions are Hoisted before the execution phase. **Hoisting** works only for *funtion declaration* not for *funtion expression*.
        ```javascript
           //Hoisting for function declarations
           console.log(sum(5, 10)); // gives 15
           function sum(num1, num2) {
               return num1 + num2;
           }

           console.log(avg(5, 10)); // gives error as 'avg is not a function'
           var avg = function (num1, num2) {
               return (num1 + num2)/2;
           }
           
           //Hoisting for variable declarations
           console.log(age); // gives undefined
           console.log(address); //give error as 'address is not defined'
           var age = 31; // without var it is not a declaration
           
           //Hoisting and Scope together
           console.log(color);     //undefined
           var color = 'red';
           function foo(){
               console.log(color); //undefined
               var color = 'green';
               console.log(color); //green
           }
           foo();
           console.log(color);     //red
        ```
    - Creation of Scope chain
      - In JavaSript scope is defined by funtion, not by *if* or *loops* unlike in other languages.
      - Each new funtion create a new scope.
      - **Lexical scope**:a function also has access to it's encolosing funtion's scope.
    - Determine the value of *this*
      - **Regular function call**: the *this* keyword points to the global object(window in browser)
      - **Method call**: the *this* keyword points to the object that is calling the method.
      - The *this* keyword is not assigned a value until the funtion which created the execution context is called.
  - **Execution phase**: 
    The code of the funtion that generated the execution context run line by line.
### Execution stack vs Scope chain
- Execution stack is determined by the order in which the funtions invoked.
- Scope chain is determined by the order in which the funtion is declared in the code.
### The *this*
  ```javascript
  console.log(this);              //window object
function sum(n1, n2){
    console.log(this);          //*
    return n1 + n2;
}
console.log(sum(1, 2));         // regular function call. * is window object

var person = {
    name : 'Shafi',
    getName: function(){
        console.log(this)       //** 
        return this.name;
    }
}
console.log(person.getName());  // method call, ** is person object

var employee = {
    printName: function(){
        var getNameLocal = person.getName;
        console.log(person.getName()); // method call, ** is person object
        console.log(getNameLocal());   // regular call, ** is window object
    },
    empName : person.getName
}

console.log(employee.empName());   // method call. ** is employee object
employee.printName();

var getName = person.getName;   
console.log(getName());         // calling execution context global context
                                // ** is window object, unexpected result
  ```
##  DOM Manipulation
### Events
Notifications that are sent when something happens on the web page.
### Event listener
Funtions that perform when certain event occures, it waits for a specific event to happen.
### Execution Stack and Message Queue
An event can be handled only after the executiuon stack become empty, which means all the funtions have returned. 
**Message queue:** this is where all the events happened that are waiting to be processed kept. when the execution stack becomes empty, the event handler corespoding to one of the event in the message queue start execute and new execution context will be created for it. once the execution completes and execution stack becomes empty again, next event from the queue will be processed. 



