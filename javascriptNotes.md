# **Javascript Notes**

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

> O/P
> Inner function is called. 
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
> O/P:
> domultiply function executed with res: 30
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

> O/P: 
> 30 
> inner one 
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
> O/P
> 100
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
> O/P
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
> O/P
> Index with let: 0
> Index with let: 1
> Index with let: 2
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
> O/P
> Index with let: 0
> Index with let: 1
> Index with let: 2
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
> O/P
> I'm var
> I'm var
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
> O/P
> I'm let
> I'm let
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
> O/P
> 100
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
> O/P
> 100 
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
  

