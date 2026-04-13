In the output of the below, the variable order will be undefined. This is because the client didn't use the new keyword.
```js
function Order(id, amount) {
  this.id = id;
  this.amount = amount;
}

const order = Order(101, 5000); 
console.log(order); // undefined
```
In order to make the code work even without new, we can do this:
1. remove the existing code inside Order function
2. create a new empty object
3. set the memebers of the fields - id,amount
4. return that object 

As such the return value of Order(101,5000) won't be undefined 

```js
function Order(id, amount) {
  let obj = {};
  obj.id = id;
  obj.amount = amount;
  return obj;
}
const order  = Order(101,5000);
console.log(order) // {id: 101, amount: 5000}
```