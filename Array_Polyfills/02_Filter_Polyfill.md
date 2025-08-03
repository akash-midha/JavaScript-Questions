# Filter Polyfill

```js
Array.prototype.myFilter = function(cb){
    if(typeof cb != 'function'){
        throw new TypeError(`${cb} is not a function`);
    }
    let result = [];
    for(let i=0 ; i<this.length; i++){
        if(i in this){      // to skip hole '2, , 3'
            if(cb(this[i],i,this)){
                result.push(this[i]);
            }
        }
    }
    return result;
}

```