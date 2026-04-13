```js
function User(name) {
  this.name = name;
}

User.prototype.skills = [];

const u1 = new User("Mrinal");
const u2 = new User("Rahul");

u1.skills.push("JS");

console.log(u2.skills)
``` 

From the above code it is clear that, since the `skills` member has been added to the User prototype, all instances of User class will share it. So if u1 modifies it, it will change for u2 as well.

To fix, this issue, convert `skills` from being a prototype member to a instance member like this 

```js
function User(name) {
  this.name = name;
  this.skills = [];
}
```
Now, `skills` have beome instance specific.