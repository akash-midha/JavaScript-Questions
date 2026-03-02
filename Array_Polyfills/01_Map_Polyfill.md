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



