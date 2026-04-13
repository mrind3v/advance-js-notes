`.__proto__` is accessible only through objects of a class/constructor. While, `.prototype` is accessible through the class/constructor only. But both point to the same thing!

e.g:
```js
function Robot() {}

Robot.prototype.greet = function() { console.log("Hello"); };

const wallE = new Robot();

// 2. The instance does NOT have .prototype
console.log(wallE.prototype); // undefined

// 3. The instance uses .__proto__ to find the blueprint
console.log(wallE.__proto__ === Robot.prototype); // true

// 4. Using the link to call the method
wallE.greet(); // "Hello"
```