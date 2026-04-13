```js
// since arg is not given as ...arg, we will assume that arg is an array - so we'll use apply instead of call/bind
function myNew(Constructor,arg) {
  let obj = {}; 
  Object.setPrototypeOf(obj,Constructor.prototype);
  let result = Constructor.apply(obj,arg);
  return (result==null) ? obj : result;
}