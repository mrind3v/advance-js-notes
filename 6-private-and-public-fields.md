In modern JavaScript, there are two primary ways to handle private and public fields: using **Classes** (the standard way) or **Closures** (the older way).

### Method 1: ES6 Classes (Standard)
Classes use the `#` prefix to make a field private. Anything without the `#` is public.

* **Public fields:** Declared normally or inside the constructor. Accessible from outside the object.
* **Private fields:** Declared with a `#`. Attempting to access them outside the class results in a syntax error.

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