# **Javascript Notes**
### Links
> https://github.com/hiteshchoudhary/js-hindi-youtube/blob/main/04_control_flow/truthy.js

## ***```1.DOM : Document Object Model```***

- DOM is a model which is actual representation of your code, it shows all your code in tree format.
- DOM is nothing but Document Object Model where
 i) Document is a file,
 ii) Object is a tag/element,
 iii) Model is a Layout structure
we can see it via console -> elements in inspect tool
- DOM is a programming interface for web documents. It represents the structure of HTML, XML, and XHTML documents as a tree-like structure where each node represents a part of the document.


## ***```2. Call Stack```***

- The call stack is a mechanism used to keep track of function calls in a program.
- Whenever a function is invoked, a new frame is pushed onto the call stack representing that function call.
- When a function completes its execution, its frame is popped off the call stack.

> In simple Words: call stack keeps track of the current execution context in a program by maintaining a stack of function calls. It helps manage the flow of control and ensures that functions are executed in the correct order.

**Example**
```
function sum() {
    // Step 2: Function sum() is invoked
    let res = sub(); // Step 3: sub() function is called
    console.log(res); // Step 8: Output the result returned by sub() function
    return res; // Step 9: Return the result
}

function sub() {
    let a = 10, b = 10; // Step 4: Define variables a and b and assign values
    var ans = a + b; // Step 5: Sum up a and b
    return ans; // Step 6: Return the sum
}

sum(); // Step 1: Call the sum() function

// Call Stack:
// 1. sum()
// 2. sub()

```
> O/P: 20

## ***```3.Function scoping / lexical scoping```***

functions defined within other functions (known as "nested functions") are only accessible within the scope of the outer function. They cannot be called from outside of the outer function.

```
function outerFunction() {
 
    function innerFunction() {
        console.log("Inner function is called.");
    }

    innerFunction(); // Call the inner function from within the outer function
console.log("Outer function is called.");
}

outerFunction(); // Call the outer function to start execution

innerFunction(); // Error: innerFunction is not defined globally
```

> O/P <br>
> Inner function is called. <br>
> Outer function is called.

```
function doadd(){
    function dosub(){
        var a = domultiply();
        document.write(" dosub function executed");
    }
    function domultiply(){
            var b = 10, c = 30;
            var res = b*c;
            document.write(domultiply function executed with res: 30);
            return(res);
    }
    dosub();
}
doadd();
```
> O/P <br>
> domultiply function executed with res: 30 <br>
> dosub function executed


## ***```Closure / nested functions / function nesting```***
In JavaScript, when you define a function within another function, the inner function has access to the outer function's variables and parameters, even after the outer function has finished executing. This is because the inner function maintains a reference to the variables of its outer function, forming a closure.
```
function mostOuterfun() {
    var a = 10;
    let b = 20;
    var res = function innerfun() {
        var sum = function innerMostfun() {
            var ans = a + b;
            document.write(ans);
            console.log("inner one")
            return ans;
        }
        sum()
        console.log("inner two");
        return a;
    }
    res();
}
mostOuterfun();
```

> O/P <br>
> 30 <br>
> inner one <br> 
> inner two 

The above procedure, where a function is defined inside another function and then called within the outer function, is commonly known as "nested functions" or "function nesting" in JavaScript.

Nested functions are functions defined within the scope of another function. They have access to the variables and parameters of their outer function and can also access global variables. However, they are not accessible outside of their outer function's scope.
function is defined inside another function in JavaScript is often referred to as "closure." A closure is a combination of a function and the lexical environment within which that function was declared. This lexical environment consists of any local variables that were in-scope at the time the closure was created.

  
# ***```Function and Block scoped```***
**Function Scope:**
- Variables declared inside a function are only accessible within that function.
- If a variable is declared inside a function using var, it is scoped to the nearest function enclosing it.
- Variables declared inside a function using var are not accessible outside of that function.
```
function fun_example() {
    {
        var a = 100;
    }
    console.log(a); // Output: 10
}
fun_example();
console.log(a); // ReferenceError: a is not defined
```
> O/P <br>
> 100 <br>
> ReferenceError: a is not defined

**Block Scope:**
- Variables declared with let and const are block-scoped.
- Block scope means that variables are only accessible within the block (enclosed by curly braces) where they are declared.
- This includes if statements, loops, and any other block enclosed by curly braces {}.
```
function blk_example() {
    {
        let a = 100;
    }
    console.log(a); // ReferenceError: a is not defined
}
blk_example();
console.log(a); // ReferenceError: a is not defined
```
> O/P <br>
> ReferenceError: a is not defined

### **Examples for Fnctional and block scoped**

```
// Using let
for (let i = 0; i < 3; i++) {
    console.log("Index with let: " + i);
}
console.log(i); //We cannot access the let outside the loop bz
//let is function scoped, it gives error like
// ReferenceError: i is not defined
```
> O/P <br>
> Index with let: 0 <br>
> Index with let: 1 <br>
> Index with let: 2 <br>
> ERROR! : ReferenceError: i is not defined

```
// Using Var
for (var j = 0; j < 3; j++) {
    console.log("Index with let: " + j);
}
console.log(j); // here it provides o/p as a 3
// here we are tring to access i after the loop,
//its value would be 3, as it's the value that caused the loop to terminate.
//This is because var doesn't have block-level scope,
//so it's not limited to just the loop.
```
> O/P <br>
> Index with let: 0 <br>
> Index with let: 1 <br>
> Index with let: 2 <br>
> 3

**Another Example for Function scoped and block scoped**
```
function abc(){
for (a=1;a<3;a++){
    console.log("I'm var");
    }
console.log("Showing a's value:", a); // a gives value where it is terminated loop
return (a);
}
abc();
```
> O/P <br>
> I'm var <br>
> I'm var <br>
> Showing a's value: 3
```
function xyz(){
   for (let b=1;b<3;b++){
    console.log("I'm let");
    }
    console.log(b); // it will result into error with 
    //ReferenceError: b is not defined
}
xyz();
```
> O/P <br>
> I'm let <br>
> I'm let <br>
> ERROR! : ReferenceError: b is not defined

# ```Can be reassigned example```
**var can be updated but cannot be re-declared into the scope…**
```
function var_example() {
    {
        var a = 100; 
        console.log(a); // Output: 100
        var a =20;
        console.log(a); // 20
    }
    
}
var_example();
```
> O/P <br>
> 100 <br>
> 20

**let can be updated but cannot be re-declared into the scope…**
```
function let_example() {
    {
        let a = 100; 
        console.log(a); // Output: 100
        let a =20;
        console.log(a); //SyntaxError: Identifier 'a' has already been declared

    }
}
let_example();
```
> O/P <br>
> 100 <br>
> SyntaxError: Identifier 'a' has already been declared

# ***```4.Difference between var,let,const```***
![alt text](https://github.com/asmi0211/javascript/blob/asmi0211-js-patch-1/images/var_let_const.jfif)
 | var | let | const |
| ------ | ------ | -----|
  |The scope of a ```var``` variable is functional scope.. |The scope of a ```let``` variable is block scope. | The scope of a ```const``` variable is block scope.  |
  |It can be ```updated and re-declared``` into the scope.. | It can be updated but cannot be re-declared into the scope.. |  It cannot be updated or re-declared into the scope. |
  |It can be declared without initialization. | It can be declared without initialization. |  It cannot be declared without initialization.. |
  |It can be accessed without initialization as its default value is “undefined”. | It cannot be accessed without initialization otherwise it will give ‘referenceError’. |  It cannot be accessed without initialization, as it cannot be declared without initialization.. |
  |hoisting done, with initializing as ‘default’ value | Hoisting is done, but not initialized (this is the reason for the error when we access the let variable before declaration/initialization |  Hoisting is done, but not initialized (this is the reason for the error when we access the const variable before declaration/initialization |
  
### ***```Hosting```***
Hoisting in JavaScript is a behavior where variable and function declarations are moved to the top of their containing scope during the compilation phase. This means that regardless of where variables and functions are declared in your code, they are processed before the code is executed.

In simpler terms, imagine JavaScript's hoisting behavior like this:
- Before your code runs, JavaScript quickly scans it and "hoists" variable and function declarations to the top.
- Variable declarations (using var, let, or const) are initialized with a value of undefined by default.
- Function declarations are completely hoisted along with their definitions.
- However, only the declarations are hoisted, not the assignments.
```
console.log(x); // undefined, because the declaration is hoisted
var x = 5;

foo(); // "Hello, I'm foo!", because the entire function declaration is hoisted
function foo() {
  console.log("Hello, I'm foo!");
}

bar(); // TypeError: bar is not a function, because only the declaration is hoisted, not the definition
var bar = function() {
  console.log("Hello, I'm bar!");
};
```
> O/P <br>
> undefined <br>
> Hello, I'm foo! <br>
> ERROR! : TypeError: bar is not a function



### ***```Data Types```*** 
![alt text](https://github.com/asmi0211/javascript/blob/asmi0211-js-patch-1/images/data-types.png)

### ***example***
```
// Numbers:
let length = 16;
let weight = 7.5;

//undefined 
let x;       // Now x is undefined
// typeof undefined is undefined
// console.log(typeof undefined);
//O/P: undefined

//null 
let x=null;       // Now x is null
// typeof null is an object
// console.log(typeof null);
// O/P: object

// Strings:
let color = "Yellow";
let lastName = "Johnson";

// Booleans
let x = true;
let y = false;

// Object:
const person = {firstName:"John", lastName:"Doe"};

// Array object:
const cars = ["Saab", "Volvo", "BMW"];

// Date object:
const date = new Date("2022-03-25");
```
 ###  ***```How to check data type```***     
 ```
  var apple = "apple";
  console.log(typeof apple); // string
  
   var number = 2052021;
  console.log(typeof number); // number
  
 typeof "John"                 // Returns "string"
typeof 3.14                   // Returns "number"
typeof NaN                    // Returns "number"
typeof false                  // Returns "boolean"
typeof [1,2,3,4]              // Returns "object"
typeof {name:'John', age:34}  // Returns "object"
typeof new Date()             // Returns "object"
typeof function () {}         // Returns "function"
typeof myCar                  // Returns "undefined" *
typeof null                   // Returns "object"
 ```
 
 ### ***```Type conversion```*** 
 - In programming, type conversion is the process of **converting data of one type to another**. For example: converting String data to Number.
 - There are two types of type conversion in JavaScript.
 - ```Implicit Conversion``` - automatic type conversion
 - ```Explicit Conversion``` - manual type conversion
 
***More Details***: https://www.programiz.com/javascript/type-conversion#google_vignette
```
// numeric string used with - , / , * results number type

let result;

result = '4' - '2'; 
console.log(result); // 2

result = '4' - 2;
console.log(result); // 2

result = '4' * 2;
console.log(result); // 8

result = '4' / 2;
console.log(result); // 2
```

 ### ***```Operators```***

JavaScript supports various types of operators, which are symbols that perform operations on operands (variables or values). Here's an overview of the different types of operators in JavaScript:

**Arithmetic Operators: These are used to perform arithmetic operations like addition, subtraction, multiplication, division, etc.**
```
+ (Addition)
- (Subtraction)
* (Multiplication)
/ (Division)
% (Modulus)
++ (Increment)
-- (Decrement)
 ``` 
**Assignment Operators: These are used to assign values to variables.**
```
= (Assignment)
+= (Addition assignment)
-= (Subtraction assignment)
*= (Multiplication assignment)
/= (Division assignment)
%= (Modulus assignment)
```
**Comparison Operators: These are used to compare two values and return a boolean result.**
```
== (Equality)
=== (Strict equality)
!= (Inequality)
!== (Strict inequality)
> (Greater than)
< (Less than)
>= (Greater than or equal to)
<= (Less than or equal to)
```
**Logical Operators: These are used to perform logical operations.**
```
&& (Logical AND)
|| (Logical OR)
! (Logical NOT)
```
**Bitwise Operators: These are used to perform bitwise operations on binary representations of numbers.**
```
& (Bitwise AND)
| (Bitwise OR)
^ (Bitwise XOR)
~ (Bitwise NOT)
<< (Left shift)
>> (Right shift)
>>> (Unsigned right shift)
```
**Unary Operators: These operate on a single operand.**
```
+ (Unary plus)
- (Unary minus)
++ (Prefix/postfix increment)
-- (Prefix/postfix decrement)
! (Logical NOT)
```
**Conditional (Ternary) Operator:** This is a shorthand for an if-else statement.
```
condition ? expr1 : expr2
String Operators:

+ (Concatenation)
```
**Type Operators:**
```
typeof (Returns a string indicating the type of the operand)
instanceof (Returns true if the object is an instance of the specified object type)
```

### ***```Dyanamically Typed```***
JavaScript is a dynamically typed language, which means that data types of variables are determined by the value they hold at runtime and can change throughout the program as we assign different values to them.


```
when we convert values to boolean

1 => true;
0 => false;
"" => false;
"abc' => true;

when we convert values to Number
"22" => 22;
"22abc" => Nan;
true => 1'
false => 0;
```
### ***```If Else Statement```***
```
var a = 100;
(a < 20) ? console.log("a is lesser") : ((a == 10) ? console.log("it's equal") : console.log("its false"))
```
> O/P: > "its false"


### ***```Switch case```***
```
switch (key)
case 1: value

	break;

case 2: value

	break;

default: 
	break;
```
**I-NOTE:** if we don't add break then all the code from match case excuted except default case, so adding break is necessary

**falsy Value**
False,0,BigInt 0n, empty string, null, undefined, NaN

**Truthy value**
empty array, empty parenthesis, "0", 'false' - beacuse it's in string, " ", [],{},function(){} - empty function

false == 0 > true
false == '' > true
0 == '' > true

### ***```Nullish Coalescing Operator (??): null undefined```***
The nullish coalescing (??) operator is a logical operator that returns its right-hand side operand when its left-hand side operand is null or undefined, and otherwise returns its left-hand side operand.

```
const foo = null ?? 'default string';
console.log(foo);
// Expected output: "default string"

const baz = 0 ?? 42;
console.log(baz);
// Expected output: 0
```
[see more](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing)

### ***```AND Operator (&&)```***
AND operator returns **True** only if **all oprands are True**, otherwise returns False.
TT=>T, otherwise F

**If both sides are True then return Right hand side**

### ***```OR Operator (||)```***
OR operator returns **False** only if **all oprands are False**, otherwise returns True.
FF=>F, otherwise T

**If both sides are False then return Left hand side**

**Note:** && excutes first before || 
