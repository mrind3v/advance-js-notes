```js
class MyPromise {
    constructor(executor) {
        this.state = "pending";
        this.value = undefined;
        this.handlers = [];
        
        const resolve = (value) => {
            if (this.state!="pending") return;
            this.state = "fulfilled";
            this.value = value;
            this.handlers.forEach(h => h.onFulfilled(value));
        }
        
        const reject = (reason) => {
            if (this.state!="pending") return;
            this.state = "rejected";
            this.value = reason;
            this.handlers.forEach(h=>h.onRejected(reason));
        }
        
        try {
            executor(resolve,reject);
        } catch (err) {
            reject(err);
        }
    }
    
    then(onFulfilled, onRejected) {
        onFulfilled = typeof onFulfilled==='function' ? onFulfilled : val=>val;
        onRejected = typeof onRejected === 'function' ? onRejected : err=>{throw err}
        
        if (this.state==='fulfilled') {
            onFulfilled(this.value);
        } else if (this.state === 'rejected') {
            onRejected(this.value);
        } else {
            this.handlers.push({onFulfilled,onRejected});
        }
        return this;
    }
    
    catch(onRejected) {
        return this.then(null,onRejected);
    }
}