# Implement Promise.allSettled function that resolves to an array of outcomes when all y=the input elements are either resolve or rejected

## Promise.all always get resolved and returns an array containing objects 
Output:
[
    { status: 'fulfilled', value: 'A' },
    { status: 'rejected', reason: 'B' },
    { status: 'fulfilled', value: 42 }
]

```javascript

export default function PromiseAllSettled(promises){
    return new Promise((resolve, reject) => {
        const results = [];

        let pending = promises.length;

        if(pending === 0){
            resolve(results);
            return;
        }

        promises.forEach((pr, idx) => {
            Promise.resolve(pr)
            .then((res)=> {
                results[idx] = {status: 'fulfilled', value: res};
            })
            .catch((err) => {
                results[idx] = {status: 'rejected', reason: err};
            })
            .finally(()=> {
                pending--;
                if(pending == 0){
                    resolve(results);
                }
            })
        })
    })
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


const result = await Promise.allSettled([p0, p1, p2]);

```