### 1. `this` inside a regular callback function 

When this is inside a callback that is passed to a web api (setTimeout) or event listener (Html), js resets this to point
to the global object (which is  undefined in strict mode)

e.g: 
```js
function Person() {
    this.age = 0;

    setInterval(function(){
        this.age++;
        console.log(age);
    })
}
```
since we are passing a regular function as callback into setTimeout, js will reset this inside it to global object. But
since the global object doesn't have an age attribute, it will be undefined 


### 2. `this` inside an arrow callback function

The value of this is inferred from the surrounding code of the arrow function 

e.g:
```js
function Person() {
    this.age = 0;

    setInterval(() => {
        this.age++;
        console.log(age);
    })
}
```
Here the value of this is taken from the surrounding code (outside the web api setTimeout). Meaning, this would be bound to
the Person object that will be created when we use the new keyword -> const person = new Person(). this would be bound to this person.

> An arrow function looks for the nearest regular function it is sitting inside. In JavaScript, an object literal {} does not create a new scope for the this keyword. Only functions create a scope that arrow functions can inherit from.