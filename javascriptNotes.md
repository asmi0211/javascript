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
