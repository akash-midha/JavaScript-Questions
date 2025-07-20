# Write a class Counter that behaves like a simple counter with the following features and method chaining:

## Requirements:
    A constructor that takes an optional initial value (default is 0)
    A method increment() that increases the count by 1
    A method decrement() that decreases the count by 1
    A method reset() that resets the count to the original initial value
    A method getCount() that returns the current count

## Example

```js
const counter = new Counter(5);

console.log(counter.getCount());  // 5
counter.increment().increment();  // count is now 7
counter.decrement();              // count is now 6
console.log(counter.getCount());  // 6
counter.reset();                  
console.log(counter.getCount());  // 5


```

## Solution

```js
class Counter{
    constructor(initialValue){
        this.initialValue = initialValue;
        this.result = initialValue;
    }

    increment(){
        this.result+=1;
        return this;
    }

    decrement(){
        this.result-=1;
        return this;
    }

    getCount(){
        return this.result;
    }

    reset(){
        this.result=this.initialValue;
        return this;
    }
}
```

## Note: Method chaining is only possible if I return this
    - If increment() returns:
    - this → you can chain the next method on the same object.
    - undefined (default if nothing is returned) → you cannot chain.

## Solution using Function and Method Chaining

```js

function Counter(initialValue){
    let result = initialValue;

    return{
       increment: function(){
            ++result;
            return this;
       },
       decrement: function(){
            --result;
            return this;
       },
       reset: function(){
            result = initialValue;
            return this;
       },
        getCount: function(){
            return result;
        }
    }


    // Below willl not work because here this isn't pointing to any object here but to global window

    // function increment(){
    //     ++result;
    //     return this;
    // }

    // function decrement(){
    //     --result;
    //     return this;
    // }

    // function getCount(){
    //     return result;
    // }

    // function reset(){
    //     result = initialValue;
    //     return this;
    // }

    // return{
    //     increment, decrement, getCount, reset
    // }
}


const counter1 = Counter(2);
console.log(counter1.increment().increment().decrement().getCount());

```



## Can you do it with arrow Functions ?

```js
function Counter(initialValue) {
    let result = initialValue;

    return {
        increment: () => {
            ++result;
            return counterAPI;
        },
        decrement: () => {
            --result;
            return counterAPI;
        },
        reset: () => {
            result = initialValue;
            return counterAPI;
        },
        getCount: () => result
    };

    // Note: We assign the returned object to a variable first 
    // so that arrow functions can refer to it via closure
    const counterAPI = {
        increment: () => {
            ++result;
            return counterAPI;
        },
        decrement: () => {
            --result;
            return counterAPI;
        },
        reset: () => {
            result = initialValue;
            return counterAPI;
        },
        getCount: () => result
    };

    return counterAPI;
}

```


## Method Chaining
    Method chaining works because each method returns the same object (this).
    This keeps the chain alive.
    Final method (like getResult()) can return a value instead of the object.


## Factory Function

A factory function is a regular function that creates and returns objects.
It's similar to a class or constructor, but it doesn't require the new keyword and can easily use closures to keep data private.

| Concept     | Factory Function               | Constructor Function         | Class                           |
| ----------- | ------------------------------ | ---------------------------- | ------------------------------- |
| Returns     | Object explicitly (`return`)   | Uses `this` (requires `new`) | Uses `this` (behind the scenes) |
| Uses `new`? | ❌ No                           | ✅ Yes                        | ✅ Yes                           |
| Closures?   | ✅ Easy                         | ❌ Not naturally              | ❌ Not naturally                 |
| Inheritance | Needs manual `Object.create()` | Can use `prototype`          | Uses `extends` + `super()`      |
