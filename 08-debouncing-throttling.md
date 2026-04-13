**Debouncing:** ensures a function runs only after a specific amount of time has passed since the last time it was called. Every time the function is triggered, the previous timer is canceled and a new one starts.

```js
function debounce(fn,delay) {
    let timer;
    return (...args) => {
        clearTimeout(timer);
        timer = setTimeout(()=>{
            func.apply(this,args);
        },delay)
    }
}
```

**Throttling:** Even if the event triggers constantly, the function only runs at the set rate. It checks the current timestamp against the last time the function ran. If the interval has passed, it executes again.

```js
function throttle(fn,interval) {
    let lastCall = 0;
    return (...args) => {
        let now = Date.now();
        if (now-lastCall>=interval) {
            lastCall = now;
            func.apply(this,args);
        }
    }
}
```