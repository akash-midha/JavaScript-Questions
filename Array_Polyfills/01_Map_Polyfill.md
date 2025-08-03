# Map Polyfill

```js
Array.prototype.myMap = function(cb){
    if(typeof cb != 'function'){
        throw new TypeError(`${cb} is not a function`);
    }
    let result = [];
    for(let i=0; i<this.length; i++){
        result.push(cb(this[i], i, this));
    }
    return result;
}

const arr = [1,2,3];
const addTwo = arr.myMap((item, i, arr) => item+2);

```

## Follow-up - Support for thisArg

```js
Array.prototype.myMap = function(cb, thisArg){
    if(typeof cb != 'function'){
        throw new TypeError(`${cb} is not a function`);
    }
    let result = [];
    for(let i=0; i<this.length; i++){
        result.push(cb.call(thisArg, this[i], i, this));
    }
    return result;    
}
```


## Follow-up - Handle Sparse Arrays 

```js
const arr = [1, , 3]; // arr[1] is a hole
```

```js
Array.prototype.myMap = function(cb){
    if(typeof cb != 'function'){
        throw new TypeError(`${cb} is not a function`);
    }
    let result = [];
    for(let i=0; i<this.length; i++){
        if(i in this){
            result.push(cb(this[i], i, this));
        }
    }
    return result;
}
```



