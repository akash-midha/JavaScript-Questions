# Implement Promise.any

Promise.any() takes an iterable of elements (usually Promises). It returns a single promise that resolves as soon as any of the elements in the iterable fulfills, with the value of the fulfilled promise. If no promises in the iterable fulfill (if all of the given elements are rejected), then the returned promise is rejected with an AggregateError, a new subclass of Error that groups together individual errors.


```javascript
export default function PromiseAny(promises) {
    return new Promise((resolve, reject) => {
        let pending = promises.length;
        const aggError = [];

        if(pending == 0){
            reject(new AggregateError(aggError, 'All promises were rejected'));
            return;
        }

        promises.forEach((pr, idx) => {
            Promise.resolve(pr)
            .then(resolve)
            .catch((err)=> {
                aggError[idx] = err;
                pending--;
                if(pending === 0){
                    reject(new AggregateError(aggError, 'All promises were rejected'));
                }

            })
        })
    })
}

```