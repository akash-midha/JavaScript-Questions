# Implement a function which converts a function f(a,b,c) to f(a)(b)(c)


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