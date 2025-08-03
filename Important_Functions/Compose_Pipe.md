# Compose

```js
function compose(...functions) {
  return function (input) {
    return functions.reduceRight((acc, fn) => fn(acc), input);
  };
}

//or simply
const compose = (...functions) => input => functions.reduceRight((acc, fn) => fn(acc), input);

```


# PIPE

```js
function pipe(...functions) {
  return function (input) {
    return functions.reduce((acc, fn) => fn(acc), input);
  };
}

//or simply
const pipe = (...functions) => input => functions.reduce((acc, fn) => fn(acc), input);

```


```js
const addTwo = (x) => x+2;
const double = (x) => x*2;

const pipeAns = pipe(addTwo, double);
pipeAns(5);  // 14


const composeAns = compose(addTwo, double);
composeAns(5);  //12
```