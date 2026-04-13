## Polyfill for Map 
```js
Array.prototype.myMap = function(cb,thisArg) {
  if (arr==null) throw new TypeError("Array is null");
  if (typeof cb !==  'function') throw new TypeError("Callback is not a function"); 
  
  let results = new Array(this.length); 
  
  for (let i=0; i<this.length; i++) {
    if (i in this) {
      results[i] = cb.call(thisArg, this[i], i, this);
    }
  }
  
  return results;
}
```
---
## Polyfill for Filter

```js
Array.prototype.myFilter = function(cb,thisArg) {
  let results = []; 
  
  for (let i=0; i<this.length; i++) {
    if (i in this) {
      if (cb.call(thisArg,this[i],i,this)) {
        results.push(this[i]);
      }
    }
  }
  return results;
}
```
---
## Polyfill for Reduce 

```js
Array,prototype.myReduce = function(cb,initVal) {
  let acc = initVal; 
  let startIdx = 0;
  let hasInitVal = arguments.length > 1

  if (!hasInitVal && this.length==0) {
    throw new TypeError("No initial value and zero length array provided!");
  }
  
  if (!hasInitVal) {
    let found = false; 
    for (let i=0; i<this.length; i++) {
      if (i in this) {
        startIdx = i + 1;
        acc = this[i];
        found = true;
        break;
      }
    }
    if (!found) {
      throw new TypeError("No fit inital value found!");
    }
  }
  
  for (let i=0; i<this.length; i++) {
    if (i in this) {
      acc = cb(acc,this[i],i,this);
    }
  }
  
  return acc;
}
```