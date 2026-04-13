## Polyfill for AllSettled 

```js
function myAllSettled(items) {
  return new Promise((resolve,reject)=>{
    let results = [];
    let completed = 0;
    if (items.length==0) {
      resolve(results);
      return;
    }
    items.forEach((promise,index)=>{
      Promise.resolve(promise).then((value)=>{
        results[index] = {status: "fulfilled",value: value};
      }).catch((err)=>{
        results[index] = {status: "rejected", value: err};
      }).finally(()=>{
        completed++;
        if (completed==items.length) {
          resolve(results);
        }
      })
    })
  })
}
```

## Polyfill for All 

Collect all resolved promises. Reject whole if even one of them fails
```js
function myAll(items) {
  return new Promise((resolve,reject)=>{
    let results = [];
    let resolved = 0;
    if (items.length==0) {
      resolve(results);
      return;
    }
    items.forEach((promise,index)=>{
      Promise.resolve(promise).then((value)=>{
          resolved++;
          results[index] = value;
          if (resolved==items.length) {
            resolve(results);
          }
      }).catch((err)=>{
        reject(err);
      })
    })
  })
}
````

## Promise for Any 

Collect all rejected promises. Resolve whole if any one of them fulfills
```js
function myAny(items) {
  return new Promise((resolve,reject)=>{
    let results = [];
    let rejected = 0;
    if (items.length==0) {
      reject(new AggregateError([],"Empty array provided!"));
      return;
    }
    
    items.forEach((promise,index)=>{
      Promise.resolve(promise).then((val)=>{
        resolve(val);
      }).catch((err)=>{
        rejected++;
        results[index] = err;
        if (rejected==items.length) {
          reject(new AggregateError(results,"All promises rejected"));
        }
      })
    })
  })
}
```


## Polyfill for Race 

```js
function myRace(items) {
  if (items.length==0) {
    return;
  }
  items.forEach((promise)=>{
    Promise.resolve(promise).then((val)=>{
      resolve(val);
    }).catch((err)=>{
      reject(err);
    })
  })
}
```