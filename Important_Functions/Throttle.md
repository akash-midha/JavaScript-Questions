# Implement a Throttle function

Throttle ensures a function is called at regular interval of time, no matter how frequently it is trigerred.

Whenever throttle function is called, I check the current time and last time it is called, if difference is greater than or equal to delay , I execute the function and update the timestamp.


```js
const throttle = (fn, delay) => {
    let last = 0;
    return function(...args){
        let now = Date.now();
        if(now-last >= delay){
            last = now;
            fn(...args);
        }
    }
}


```