# Implement a debounce function

Debouncing ensures that function is called only once after ceratin period of time since the last call, even if it is trigerred multiple times in succession.

Every time the returned function is called, I clear the previous timer and create a new one. If no new call happens within the delay, the function finally executes.

```js
const debounce = (cb, delay) => {
    let timer;
    return function(...args){
        clearTimeout(timer);
        timer = setTimeout(()=> {
            cb(...args);
    }, delay);
    }
}

```
