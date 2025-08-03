# Reduce Polyfill

```js
Array.prototype.myReduce = function(cb, initialValue){
    if (typeof cb !== 'function') {
        throw new TypeError(cb + ' is not a function');
    }
    if(this.length < 1 && initialValue == undefined){
        throw new TypeError('Array is empty');
    }
    else if(this.length < 1){
        return initialValue;
    }
    let sI = 0;
    if(initialValue == undefined){
        initialValue = this[0];
        sI = 1;
    }

    let acc = initialValue;

    for(let i = sI; i<this.length; i++){
        if(i in this){
            acc = cb(acc, this[i], i, this);
        }
    }
    return acc;
}

```
This will fail here - 

[ , , 5].reduce((a, b) => a + b); // ✅ 5
[ , , 5].myReduce((a, b) => a + b); // ❌ TypeError: Array is empty

## Follow-up -? What if we call it on an empty array , write the logic
