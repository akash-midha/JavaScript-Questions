# Implement a function which converts a function f(a,b,c) to f(a)(b)(c)


<!-- I use the function's length to determine how many arguments are required. I keep collecting arguments through closures, and once I have enough arguments, I invoke the original function. -->

```js
function curry(func){
    return function curried(...args){
        if(args.length >= func.length){
            return func(...args)
        }
        else{
            return function(...next){
                return curried(...args, ...next)
            }
        }
    }
}

```