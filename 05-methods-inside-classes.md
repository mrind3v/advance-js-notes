Methods present inside classes creates using the `class` keyword in js are by default inside the prototype of the class

e.g:

```js
class User {
  constructor(name) {
    this.name = name;
  }

  greet() {
    return `Hello, ${this.name}`;
  }
}
```

In the above code, greet() method is by default created inside the User prototype