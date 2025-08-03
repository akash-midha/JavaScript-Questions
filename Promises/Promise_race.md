# Promise.race

## Implement Promise.race() function that resolves or rejects when any of the input elements are reolved or rejected

```javaScript
Promise.racePolyfill = (promises) => {
    return new Promise((resolve, reject) => {
        if(promises.length == 0){
            return;
        }

        promises.forEach((pr, idx) => {
            Promise.resolve(pr)
            .then(resolve)
            .catch(reject);
        })
    });
}
```


## Example


```javascript
const p0 = 20;
const p1 = Promise.reject('P1 rejected');
const p2 = new Promise ((resolve,reject) => {
    setTimeout(()=> {
        resolve('P2 resolved');
    },100)
});


const result = await Promise.race([p0, p1, p2]);
```