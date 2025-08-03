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

## Give access of this

```js
const debounce = (cb, delay) => {
    let timer;
    return function(...args){
        clearTimeout(timer);
        timer = setTimeout(()=> {
            cb.apply(this, args);
    }, delay);
    }
}
```


## Follow up - Debounce with a cancel() method to cancel delayed invocations and a flush() method to immediately invoke them.

```js
const debounce = (cb, delay) => {
    let timer = null;
    let lastArgs = null;
    let lastThis = null;

    function debounced(...args){
        lastArgs = args;
        lastThis = this;

        if(timer) clearTimeout(timer);

        timer = setTimeout(()=> {
            cb.apply(lastThis, lastArgs);
            timer = null;
            lastArgs = null;
            lastThis = null;
        }, delay);
    }

    debounced.cancel = function(){
        if(timer){
            clearTimeout(timer);
            timer = null;
            lastArgs = null;
            lastThis = null;
        }
    }

    debounced.flush = function(){
        if(timer){
            clearTimeout(timer);
            cb.apply(lastThis, lastArgs);
            timer = null;
            lastArgs = null;
            lastThis = null;
        } 
    }

    return debounced;
}


```


## Follow up - Debounce w
