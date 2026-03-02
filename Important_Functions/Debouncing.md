# Implement a debounce function


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
