We will make an alternative way for a class to extend some other class through prototype chaining 

Say there already exists a User class with some properties and methods
```js
function User(name) {
  this.name = name;
}

User.prototype.login = function () {
  return `${this.name} logged in`;
};
```

Now we want to have a class Admin to have all the features (properties and methods) of User + some extra features - like a method deleteUser.

```js
function Admin(name) {
    // we call the User constructor here so that admin also has the same fields as User
    User.call(this,name);
}

// next we inherit the methods inside the User prototype over to Admin 
Object.setPrototypeOf(Admin.prototype, User.prototype); 

Admin.prototype.deleteUser = function() {
    return `${this.name} deleted...`
}
```