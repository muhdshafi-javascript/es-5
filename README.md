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
```
Re-assigning the value to variable is calle **Variable Mutation**, javaScript dynamically change type based on the new value assigned.
```javascript
var age = 31;
console.log(typeof age, age);//number
 age = '31';
console.log(typeof age, age);//string
```
