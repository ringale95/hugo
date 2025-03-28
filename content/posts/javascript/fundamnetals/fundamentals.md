+++
date = '2025-02-16T06:59:55-05:00'
draft = true
title = 'Fundamentals'
+++

## JS Fundamentals

The `<script>`tag contains JS code which can be automatically executed when browser processes the tag.

Inside script we can specify JS modules. Simple scripts are wriiten html whereas complex scripts reside in separate file. Browser can download it and cache it so whenever other pages reference the same script it will take from cache instead of downloading it again. This reduces traffic and makes pages faster

Below is invalid :

```
<script src="file.js">
  alert(1); // the content is ignored, because src is set
</script>
```
## use strict

In JS line break implicitly considers it as semicolon. Even if there is no semicolon but a line break it will terminate the sentence

To enable modern JS programming rules .which prevent common mistakes put **use strict** in the code. It helps catch silent errors and enforces best practices. Example:

```
"use strict";
x = 5; // Error: x is not defined

```
### Should we use use strict?
Modern JavaScript supports “classes” and “modules” – advanced language structures (we’ll surely get to them), that enable use strict automatically. So we don’t need to add the "use strict" directive, if we use them.

## Variables:

A variable is named storage for data.

Create or declare a variable by:
```
let message;
```

Put some data into it:
```
message = "hello"
```

Access it :
```
alert(message);
```

Declare multiple variable in one line:
```
let user = 'John', age = 5, message = 'Hello';
```
![alt](/variable.png)

Declaring variable twice triggers an error:
```
let message = 'This'
let message = 'That'
```
Gives error that message is already declared.

Functions are classified as pure or impure based on behavior. A pure function produce same output for the same input. Does not modify external state

Example of pure function:
```
    function add(a,b){
        return a + b;
    }
```

Impure functions relies on external state and return different results based on same input

Example for impure functions:
```
let sum = 0;
function addToSum(val){
    sum += val;
    return sum;
}
```
## Limitation on variable naming
- Name must contain letters, digits, symbols
- First character must not be a digit
- '$' and '_' can be used in names
- Hyphens not allowed
- case sensitive so 'name' and 'Name' are two different things
- Reserved keywords not allowed


```
//Without use strict
num = 5;   // will create num variable

// With use strict
"use strict";
num = 5   ❌ Error:  // will give error to declare it or num is not defined
```

```
let x; // Declares a variable 'x' without assigning a value
var y; // Declares a variable 'y' without assigning a value
const z; // ❌ Error: 'const' variables must be assigned a value at declaration
```

```
let a = 10; // Declares and assigns → Definition
var b = "Hello"; // Declares and assigns → Definition
const c = true; // Declares and assigns → Definition
```

## Constant

To declare a constant variable use `const` instead of `let`
```
const myBD = '12.07';
myBD = 23432 // ❌ Error: 'const' variables cannot be reassigned
```

`alert()` is browser specific and not node

## Data Types

JS is dynamically typed language means a variable at one moment can store string as well as number.

There are 7 primitive data types:
- number (integer or floating point)
- bigint (integer numbers of arbitrary length)
- string
- boolean
- null
- undefined for unassigned values
- symbol

There is 1 non-primitive type:
- Object

***type of*** operator allows to see which type is stored in a variable

## Browser interaction Javascript
1. alert
2. prompt
3. confirm

```
alert("Hello")
```
prompt:

```
let age = prompt('How old are you?', 100);
alert(`You are ${age} years old.`)
```

![alt](/prompt.png);

confirm:
```
let isBoss = confirm("Are you the boss?");
alert(isBoss);
```

Above returns true if clicked on OK, else returns false if clicked on 'Cancel'

```
<!DOCTYPE html>
<html>
<body>

  <script>
    'use strict';

    let name = prompt("What is your name?", "");
    alert(`Your name is ${name}`);
  </script>

</body>
</html>
```

## Type Conversions

1. String conversions
   ```
   let value = true
    value = String(value)
   ```

2. Number Conversion
   ```
    let str = "123";
    lleet num = Number(str);
    console.log(typeof num) // Number
   ```

**String concatenation with '+'**
```
let s = "my" + "string";
console.log(s); // mystring;

console.log('1' + 2) //12

console.log(2+2+'1')  // 41

let apples = "2"
let oranges = "3"
alert(apples + oranges) //23
```

```
let apples = "2"
alert(+apples) // Here +apples will convert string to number
```

**Precedance of operators:**
- Unary plus or minus
- Exponentiation
- Multiplication, Divsiion
- Addition,  Subtration

```
Modify and assign operators: 
let n = 2;
n *= 3+5;
console.log(n) // 16

let counter = 2;
counter++;
alert(counter); // 3

let counter = 2;
counter--;
alert(counter) // 1


let counter = 1;
let a = ++counter; //Increase value immediately and returns 2
let a = counter++;   // Increase value later
alert(a)
```

Post-Increment (a++)
Returns the original value of a before incrementing.
Then increments a by 1.
```
let a = 5;
let b = a++; // b gets the original value of a (5), then a becomes 6

console.log(a); // 6
console.log(b); // 5
```

2. Pre-Increment (++a)
Increments a by 1 first.
Then returns the new incremented value.
```
let a = 5;
let b = ++a; // a is incremented to 6, then b gets 6

console.log(a); // 6
console.log(b); // 6

````

```
"" + 1 + 0 = "10"
"" - 1 + 0 = -1
true + false = 1
6/"3" = 2
"2" *"3" = 6
4+5+"px" = 9px
"$" + 4 + 5 = "$45"
"4" - 2 =2
"4px" - 2 = NaN
"-9 " + 5 = " -9 5 "
" -9 " - 5 = 14
null + 1 = 1
undefined + 1 = NaN
"\t \n" -2 = -2
```

## Comparison operators:
- Greater than/ Less than
- Greater or less than equals to
- Equals (== means equality test), (= means an assignment)
- Not equal to
  

  - true : yes, correct, the truth
  - false: no, wrong, not the truth

- string comparison are done lexicographical

### Comparison of different types.
```
alert('2' > 1); // Here string becomes number
alert(true == 1) // Here true becomes 1
```

### Strict equality : checks value and type meaning operands must be of same type
```
alert(0 === false)     // false

alert('' === false)    // false. An empty string just like false becomes zero. Operands are converted to numbers by equality

alert(null === undefined);  //false
```
### Non strick check : allows type conversion before comparison
```
alert(null == undefined);       //true

alert( null > 0 )  //false
```

**null is only equal to undefined and nothing else. While comparing javascript converts null to '0' so:**
```
null >= 0   //true
```
For undefined:
```
undefined > 0; //false
undefined < 0; //false
undefined == 0; //false
```
**As compare anything with undefined it returns NAN**

```
5 > 4 //true
"apple" > "pineapple" // false
"2" > "12" //false
undefined == null  //true
undefined === null  //false
null == "0" //false
nul === 0 //false
null >= 0 //true
```
For comparison,
== -> loosely typed (converts values to same type before comparing)
    Example:
    ```
    console.log(5 == '5'); //true
    console.log(null == undefined) //true
    ```
=== -> strict equality (no type conversion. Values must be of same type and value to return true)
    Example:
    ```
    console.log(5 === '5'); //false
    console.log(null === undefined) //false
    console.log(0 == false); //false

    ```


## Conditional branching
if() statement evaluates a condition and if it is true, executes a block of code

```
if(year == 2015) alert("You are right!")
```

`else if`:
```
let year = prompt('In which year was the ECMAScript-2015 specification published?', '');

if (year < 2015) {
  alert( 'Too early...' );
} else if (year > 2015) {
  alert( 'Too late' );
} else {
  alert( 'Exactly!' );
}
```

`Conditional operator (?)`:

```
let result = conditon ? value 1 : value 2

Example:
let accessallowed = age > 18 ?   true: false
```

```
if ("0") console.log("0 is string");        // true
if(0) console.log(" 0 is number ");         // false
``` 

### Logical operators
There are 4 logical operators in JS:
1. OR
2. AND
3. NOT
4. Nullish Coalescing

OR: if one of argument is **true** it returns true otherwise **false**

```
true || true : true
true || false: true
false || true : true
false || false : false
```

```
if(1 || 0) return true;

alert("FirstName" || "LastName" || "Anonymous") // if the FirstName, LastName are falsy, "Anonymous" will show up
```
**Short circuit evaluation:**
|| processess its argument until the first truthy value is reached, and then the value is returned immediately without even touching the other argument
```
true || alert("not printed"); 
```

**&& operator**

&& -> returns true if both operations are true else return falsy. If all operands have been evaluated (i.e. all were truthy), returns the last operand.

**In other words, AND returns the first falsy value or the last value if none were found**

```
alert( true && true );   // true
alert( false && true );  // false
alert( true && false );  // false
alert( false && false ); // false
```
Below returns true or false and not day:
```
let day = 2;
if (day = 2 && day > 1) {
    console.log(day);
}
``` 

**NOT ! operator**

- Converts a value to boolean
```
console.log(!true);  // false
console.log(!false); // true
console.log(!0);     // true  (0 is falsy, so !0 becomes true)
console.log(!1);     // false (1 is truthy, so !1 becomes false)
console.log(!"hello"); // false (non-empty strings are truthy)
console.log(!"");      // true (empty string is falsy)
console.log(!null);    // true (null is falsy)
```


Using !! (double NOT) forces any value to a boolean:

The first ! converts the value to true or false, but inverts it.
The second ! flips it back to its original boolean meaning.

! operator has highest precedence.


**The Switch Statement**

A switch statement replace multiple `if` statements

```
switch(x){
    case: 'value1':
        ....
    break;

    case: 'value2':
        ....
    break;

    default:
        ...
    break;
}
```

```
let a = "1";
let b = 0;

switch(+a){
    case b + 1:
        alert("runs as +a = 1 which is equal to b + 1");
    break;

    default:
        alert("This does not run!");
}
```

## Nullish coalescing operator '??'
?? returns first argument if its not null/undefined otherwise the second one.

```
result = a ?? b
```
return a if defined else b

Below we show user if user is not null/undefined, otherwise we show "Anonymous"
```
let user;
alert(user ?? "Anonymous")


let firstName = null;
let secondName = null;
let nickName = "Supercoder";

alert(firstName ?? secondName ?? nickName ?? "Anonymous")
```
?? is similar to ||. Only difference is :

|| returns the first truthy value. In other words, || doesn’t distinguish between false, 0, an empty string "" and null/undefined. They are all the same – falsy values.
?? returns the first defined value.

```

let height = 0;

alert(height || 100); // 100
alert(height ?? 100); // 0

```


## Functions:
Functions are the main “building blocks” of the program. They allow the code to be called many times without repetition.

```
function name(parameter1, parameter2, ... parameterN) {
 // body
}
```

A function can access outer variable as well:
```
let name = "John";
function showMessage(){
    let message = "Hello," + name;
    console.log(message)
}
showMessage();
```

A **parameter** is the variable listed inside the parentheses in the function declaration (it’s a declaration time term).

An **argument** is the value that is passed to the function when it is called (it’s a call time term).

Default value passing:
```
function showMessage(from, text = "no text given") {
  alert( from + ": " + text );
}

// can pass function too
function showMessage(from, text = anotherfunction()) {
  alert( from + ": " + text );
}
```

**Return** in function:

The directive **return** can be in any place of the function. When the execution reaches it, the function stops, and the value is returned to the calling code (assigned to result above).
```
function sum(a,b){
    return a+b; // When execution reaches it function stops and the value is returned to the calling code
}
```
### Functional expressions

```
let sayHi = function(){
    alert("Hello!");
}
```

Function Declarations are hoisted. Meaning Javascript processes function declaration first making them available throughout the script
```
sayHi("John");
function sayHi(name){
  alert(`Hello, ${name}`);
}
```

Function expressions are not hosited. They can't be called before they are hoisted
```
sayHi("John"); // ❌ Error: sayHi is not defined yet

let sayHi = function(name) {
  alert(`Hello, ${name}`);
};

```

To handle strings we have **Template literals**
String interpolation
embedded expression: You can execute Javascript inside ${}
```
let name = "Raveena";
let greeting = `Hello, ${name}`;

let a = 5, b =10;
console.log(`Sum of a and b ${a+b}`);
```

## Arrow functions
```
let func = (arg1, arg2) => expression;

let func = function(arg1, arg2){
  return expression;
}

let sum = (a,b) => a+b;  //this directly returns no need to write return, if we use curly braces we need to explicitly return

let sum = (a,b) =>{
  let result = a+b;
  return result;
}
 ```

## Loops
while Loop:
```
while(condition){}
```

While the condition is truthy, the code from the loop is executed

```
let i = 0;
while(i<3){
  alert(i);
  i++;
}


let i = 3;
while(i){      // when i = 0; it is falsy so stops answer is 3,2,1
  alert(i);
  i--;
}
```

Do-while loops:
If we want to first execute the loop and then check the condition
```
let i = 0;
do {
  alert( i );
  i++;
} while (i < 3);
```

**Continue**

Continue does not stop the loop like 'break'. Instead if stops the current iteration and move to next
```
for(int i = 0; i< 10; i++){
  if(i % 2 == 0)
}
```
```
Break/Continue cannot be added to coding statement with '?'
```

## Lexical scope
Lexical scope defines accessibility of variables and functions depending on their location in source code.
In simple terms, lexical scope means where the variable is written and not from where it is called.

Dynamic scope: Means that variables are stored in callstack and  it always look for variable in calling function scope

**Example for Lexical Scope:**
```
function outer(){
  let x = 10;   // x is defined inside outer()

  function inner(){
    console.log(x);   // inner can access x due to lexical scope
  }
  return inner;
}
const fn = outer();
fn();
```

**Example for Dynamic Scope:**
```
let x = 10;
function foo(){
  console.log(x); // Looks for x in the calling function's scope
}
function(bar){
  let x = 20;
  foo();   // If JavaScript had dynamic scope, this would print 20
}
bar();
```

- Global scope : Variables defined outside of function or block accessible anywhere in program.
- Local scope : Variables defined inside a funciton or block accessible only within the function or block
- Nested scope : Inner function have access to variable in their parent function
- Block scope: Variables declared with 'let' and 'const' are limited to block they are declared in

## Closures
Function has a reference to all variables declared in same scope as well as any outer function scopes even after the function finished execution.
Means Inner function has access to any variable declared above it.

```
function outer(){
  let outerVar = 'Outer scope';
  function inner(){
    console.log(outerVar);
  }
  return inner;
}

const closure = outer();
closure();
```

CLOSURES can make the variable private and has access only to specific function.

```
function counter() {
  let count = 0;  // Local variable (only accessible inside counter function)

  return function() {  // Inner function (closure)
    count++;   // Increment count
    return count;
  };
}

const increment = counter();  // Call counter() and store returned function
console.log(increment());  // Output: 1
console.log(increment());  // Output: 2
console.log(increment());  // Output: 3

```

Here count is accessed in function and returned when counter() is called it returns function and stores in increment variable
but the function is not yet executed. When increment() is called then the function is executd and increments count.

Now Step by step execution:
 - calling counter();
     - creates local variable count and sets to '0';
     - returns inner function(closure) but does not execute it yet
 -  Storing closure in increment
 -  calling increment 
    -  inner function executes 
    -  count++ increments from 0 to 1
    -  1 is returned
  

  Normally, the local variables are destroyed once function execution completes but when a function is a closure it retains the value even after the 
  function execution finishes. it does not garbage collect it.

  Whereas Higher order function returns a function but does not remember the local variable.



------------------------------------------------------------

## Objects:
There are 8 data types in Javascript. 7 are primitive as their values contain only single thing. 
Objects are used to store keyed collections of various data and more complex entities

Key: string
value: anything
```
{
  key: value        //Here key is name/identifier
}
```

Two ways to create an object:
```
let user = new Object();
```

```
let user = {}
```

Example:
```
let user = {
  name: "John",
  age: 20
}
```
![alt](/obj.png)

**Delete operator:**

To remove a property from object use:
```
delete user.age;
```
![alt](/obj2.png)

Multiword property names: Must be quoted
```
let user ={
  name: "John",
  age:30
  "likes birds": true //multiword property
}

. access does not work for multiword: Use square brackets
user["likes birds"] = true;
```
![alt](/obj3.png)

In short square bracket notation help to access property dynamically whereas dot notation use to access  when we know the property name at the time of writing code and is valid.

Dynamic property access means use variable to store the property instead of directly accessing
```
const key = "name";
const user = {
  name: "Raveena",
  age: 20
}
console.log(user[key]);


const student = {
  name: "Raveena",
  age: 25,
  course: "Web dev"
}

for(let key in student)
  console.log(`${key} in ${student[key]}`);
```

Computed properties:

- Use square brackets in an object literal, when creating an object.
  
```  
  let fruit = prompt("Which fruit to buy?", "apple");
  let bag = {
    [fruit]: 5
  }
  alert(bag.apple);
```
let fruit = prompt("Which fruit to buy?", "apple");
let bag = {};
bag[fruit] = 5;

If property and value are of same name just use one:
```
let user = {
  name: name,
  age: age
}

//Instead write this:
let user ={
  name,
  age
}
```

```
let person = {};
person.name = "John";
person.surname = "Smith";
person.name = "Pete";
let key = "name";
delete person.name;
console.log(person);
```

## Object referencing and copying:

**Objects** are stored and copied as **reference** whereas **primitive** values are copied as **whole number**

![alt](/objreference.png)

Two memory types:
Stack memory : All the primitive values and references are stored
Heap memory: All the actual object is stored

Object is stored somewhere in memory and user variable has reference to the object. So when the object variable is copied, the reference is copied but not the object itself is not duplicated

```
let user = {name: "Raveena"};
let admin = user;
```
![alt](/ref.png)

We can use either user or admin to access or modify properties of object

Two objects are equal if they point or reference to same object otherwise they are not:
```
let a = {};
let b = a       
alert(a==b)    // true

let a = {};
let b = {};
alert(a == b)     //false
```

```
const user = {
  name: "Raveena"
}

user.name = "Ing"         // does not give error because the object user pointing to is constant but the values can still be modified
```

## Cloning and merging
To duplicate an object we can create  a new object and replciate the structure

```
let user = {
  name: "Raveena",
  age: 28
}

let clone = {};

for(ley key in user){
  clone[key] = user[key];
}

clone.name = "Pete";
alert(user.name);
```

OR use method **assign**
Object.assign(dest, sources)

### Shallow copy vs Deep copy
- Shallow copy just copy the primitive values directly but the nested object remains same. 
  - Meaning copy only the top-level reference of object to a new variable while nested object still reference the original memory location. So if you change the nested properties in one of object it will reflect in another as they still share same memory reference
  
- Deep copy duplicates everything including nested objects ensuring copy is fully dependent. It creates independent new object and any changes made to one does not affect another
