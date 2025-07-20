# Flatten array 

```js
const arr = [1, [2, 3], [4, [5, 6, [7], 8], 9]];
flatten(arr); // [1,2,3,4,5,6,7,8,9]
```

## Solution

```js
function flatten(arr){
    let result = [];

    for(let item of arr){
        if(Array.isArray(item)){
            result.push(...flatten(item));
        }
        else{
            result.push(item);
        }
    }
    return result;
}
```

Time Complexity - O(n) -> n = no. of items in array

## Using Array.prototype

```js
Array.prototype.flat = function(){
    let result = [];

    for(let item of this){
        if(Array.isArray(item)){
            result.push(...item.flat());
        }
        else{
            result.push(item);
        }
    }
    return result;
}
```


# Flatten Only one level


```js
function flatten(arr){
    let result = [];

    for(let item of arr){
        if(Array.isArray(item)){
            result.push(...item);
        }
        else{
            result.push(item);
        }
    }
    return result;
}

```


## When depth is given

```js
Array.prototype.flattenWithDepth = function(depth = 1){
    let result = [];

    for(let item of this){
        if(Array.isArray(item) && depth > 0){
            result.push(...item.flattenWithDepth(depth-1));
        }
        else{
            result.push(item);
        }
    }
    return result;
}
```

### Example

```js
[1, [2, [3, [4, [5]]]]].flattenWithDepth(1);
// Output: [1, 2, [3, [4, [5]]]]

[1, [2, [3, [4, [5]]]]].flattenWithDepth(2);
// Output: [1, 2, 3, [4, [5]]]

[1, [2, [3, [4, [5]]]]].flattenWithDepth(Infinity);
// Output: [1, 2, 3, 4, 5]
```
