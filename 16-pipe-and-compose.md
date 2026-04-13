## Pipe 
Pipe executes fns from left to right 
```js
function myPipe(...fns) {
  return function(x) {
    return fns.reduce((acc,fn)=>{
      return fn(acc);
    },x);
  }
}
```
---
## Compose 
Compose executes fns from right to left 
```js
function myCompose(...fns) {
  return function(x) {
    return fns.reduceRight((acc,fn)=>{
      return fn(acc);
    },x)
  }
}
```