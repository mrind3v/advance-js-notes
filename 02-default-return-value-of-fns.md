By default, all functions in js returns undefined unless you explicitly return something
or it is an object  

e.g:
```js
function Order(id, amount) {
  this.id = id;
  this.amount = amount;
}

const order = Order(101, 5000);
console.log(order);
```

In the above code order will by undefined. Also, it is not an object as we didn't use the new
keyword to do `const order = new Order(101,5000)`, so don't expect logged value of order should
be an object