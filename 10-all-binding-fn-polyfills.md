## Polyfill for Call

```js
Function.prototype.myCall = function(context,...args) {
    // Use a unique symbol to avoid overwriting existing properties of
    // the context object
    let fnKey = Symbol(); 
    // note that this refers to the function that calls myCall -> i.e func is this if we do func.myCall(context,a1,a2)
    context[fnKey] = this;
    let result = context[fnKey](...args);
    // delete the function at fnKey, so the original context obj remains the same 
    delete context[fnKey];
    return result;
}
```
Eg: `func.myCall(thisObj, arg1, arg2)`

---

## Polyfill for Apply 

```js
Function.prototype.myApply = function(context,args=[]) {
 let fnKey = Symbol();
context[fnKey] = this;
let result = context[fnKey](...args);
delete context[fnKey];
return result;
}
```
Eg: `func.myApply(thisObj,[arg1,arg2])`

>Note: The final execution context[fnKey](...args) evaluates to the exact same result in both polyfills even though we pass arguments to myApply and myCall differently
---
## Polyfill for Bind 

```js
Function.prototype.myBind = function(context,...args) {
  let orgFn = this;
  return function(...newArgs) {
    return orgFn.apply(context,[...args,...newArgs]);
  }
}
```
