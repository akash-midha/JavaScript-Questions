# Implement a JavaScript function named calculator that will return an object with methods for the basic arithmetic operations. Each method will modify the incoming input variable and will return the object itself to enable method chaining.


## Example

```js
//invoking the below chainable calc function should output the result 50. 
calculator().add(10).subtract(5).multiply(20).divide(2).getResult();
```

## Solution

```js

function calculator(initialValue = 0) {
    let result = initialValue;
    const originalValue = initialValue;
    const memory = {};
    const operations = [];

    const log = (op, value) => operations.push(`${op}(${value}) => ${result}`);

    return {
        add(num) {
            result += num;
            log('add', num);
            return this;
        },
        subtract(num) {
            result -= num;
            log('subtract', num);
            return this;
        },
        multiply(num) {
            result *= num;
            log('multiply', num);
            return this;
        },
        divide(num) {
            if (num === 0) {
                throw new Error("Cannot divide by zero");
            }
            result /= num;
            log('divide', num);
            return this;
        },
        power(num) {
            result = Math.pow(result, num);
            log('power', num);
            return this;
        },
        reset() {
            result = originalValue;
            log('reset', originalValue);
            return this;
        },
        fix(n) {
            result = parseFloat(result.toFixed(n));
            log('fix', n);
            return this;
        },
        store(name) {
            memory[name] = result;
            log('store', `${name} = ${result}`);
            return this;
        },
        recall(name) {
            if (!(name in memory)) {
                throw new Error(`No memory stored under name: ${name}`);
            }
            result = memory[name];
            log('recall', name);
            return this;
        },
        clearMemory() {
            for (let key in memory) delete memory[key];
            operations.push('clearMemory');
            return this;
        },
        history() {
            return [...operations];
        },
        getResult() {
            return result;
        }
    };
}

const calc = calculator(5).add(2).subtract(1).multiply(2).getResult();
```




## Solution Using Class

```js
 
class Calculator{

    constructor(initialValue = 0){
        this.result = initialValue;
    }

    add(num){
        this.result +=num;
        return this;
    }

    subtract(num){
        this.result-=num;
        return this;
    }

    multiply(num){
        this.result*=num;
        return this;
    }

    divide(num){
        if (num === 0) {
            throw new Error("Cannot divide by zero");
        }
        this.result/=num;
        return this;
    }

    getResult(){
        return this.result;
    }
};

const calc = new Calculator(10);

const result = calc
  .add(5)         // 15
  .subtract(3)    // 12
  .multiply(2)    // 24
  .divide(4)      // 6
  .getResult();   // returns 6

console.log(result); // 6
```

| Feature              | Function-Based           | Class-Based             |
| -------------------- | ------------------------ | ----------------------- |
| More functional      | ✅ Yes                    | ❌ Less preferred        |
| Reusability via OOP  | ❌ Limited                | ✅ Inheritance/Extension |
| Method Chaining      | ✅ Possible               | ✅ Possible              |
| Good for Complex App | ❌ Harder to manage state | ✅ Better Encapsulation  |
