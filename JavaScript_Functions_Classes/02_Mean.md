# Mean

## Implement a function mean(array) that returns the mean (also known as average) of the values inside array, which is an array of numbers.

### Example

```js
mean([4, 2, 8, 6]); // => 5
mean([1, 2, 3, 4]); // => 2.5
mean([1, 2, 2]); // => 1.6666666666666667
```

### Solution

```js
export default function mean(array){
    if(!Array.isArray(array)){
        throw new Error('It is not an error');
    }

    const sum = array.reduce((acc, item) => (acc = acc+item), 0);
    const ans = sum/array.length;
    return ans;
}
```

