# Implement Promise.all

```javascript

export default function PromiseAllPolyfill(promises) {
    return new Promise ((resolve, reject) => {
        const results = [];

        if(!promises.length){
            resolve(results);
        }

        let pending = promises.length;

        promises.forEach((pr, idx) => {
            Promise.resolve(pr)
            .then((res) => {
                results[idx] = res;
                pending--;
                if(pending == 0){
                    resolve(results);
                }
            })
            .catch(reject);
        })
    })
}

```

```javascript
// Resolved example.
const p0 = Promise.resolve(3);
const p1 = 42;
const p2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('foo');
  }, 100);
});

await promiseAll([p0, p1, p2]); // [3, 42, 'foo']



// Rejection example.
const p0 = Promise.resolve(30);
const p1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject('An error occurred!');
  }, 100);
});

try {
  await promiseAll([p0, p1]);
} catch (err) {
  console.log(err); // 'An error occurred!'
}
```