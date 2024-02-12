# Javascript Notes

### DOM : **Document Object Model**
```
DOM is nothing but Document Object Model where
Document is a file, Object is a tag/element,Model is a Layout structure
DOM is a model which is actual representation of your code, it shows all your code in tree format
we can see it via console -> elements in inspect tool
```

### Call Stack
```
the call stack is a mechanism used to keep track of function calls in a program.
Whenever a function is invoked, a new frame is pushed onto the call stack representing that function call.
When a function completes its execution, its frame is popped off the call stack.
```
```
In simple Words: call stack keeps track of the current execution context in a program by maintaining
a stack of function calls. It helps manage the flow of control and ensures that functions
are executed in the correct order.
```
Example
```
function sum(){
    let res = sub();
    console.log(res);
    return(res);
}
function sub(){
    let a = 10, b = 10;
    var ans = a+b;
    return(ans);
}
sum();
```
> o/p: 20

### Function scoping / lexical scoping
```
functions defined within other functions (known as "nested functions") are only accessible within
the scope of the outer function. They cannot be called from outside of the outer function.
```
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

O/P
> Inner function is called. <br>
> Outer function is called.

```
function doadd(){
    function dosub(){
        var a = domultiply();
        document.write(" dosub");
    }
    function domultiply(){
            var b = 10, c = 30;
            var res = b*c;
            document.write(res);
            return(res);
    }
    dosub();
}
doadd();
```
O/P:
> 300 dosub
