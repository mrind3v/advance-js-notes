In modern JavaScript, there are two primary ways to handle private and public members: using **Classes** (the standard way) or **Closures** (the older way).

### Method 1: ES6 Classes (Standard)
Classes use the `#` prefix to make a member private. Anything without the `#` is public.

```javascript
class User {
  // Private field
  #password; 

  constructor(name, password) {
    this.name = name;      // Public field
    this.#password = password;
  }

  // Public method can access private fields
  checkPassword(input) {
    return input === this.#password;
  }
  // private method 
  #anotherFn(input) {
    // do something
  }
}

const me = new User("Alice", "1234");
console.log(me.name);      // "Alice"
console.log(me.#password); // Syntax Error
```

### Method 2: Closures (Function Scope)
This uses a function to "hide" variables. Only methods defined inside that function can see the local variables.

* **Public fields:** Properties attached to the returned object using `this` or as key-value pairs.
* **Private fields:** Local variables declared with `let` or `const` inside the function.

```javascript
function CreateUser(name, password) {
  let secret = password; // Private variable

  return {
    name: name,          // Public property
    getSecret: function() {
      return secret;     // Accesses private variable
    }
  };
}

const me = CreateUser("Alice", "1234");
console.log(me.name);   // "Alice"
console.log(me.secret); // undefined
```

### Prototype and Instance Members
In JavaScript classes, members are public by default unless you specifically use a hashtag # prefix to make them private.

##### Methods
**Outside the constructor:** These are public prototype methods. They are shared by all instances of the class.

**Inside the constructor:** Defining a method here (e.g., this.myMethod = function() {}) makes it a public instance method. It is recreated every time a new object is made, which uses more memory than a prototype method.

##### Fields
**Outside the constructor:** Known as "class fields," these are public by default.

**Inside the constructor:** Any variable attached to this (e.g., this.name = 'John') is a public instance field.
