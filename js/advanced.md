# Advanced topic

# Table of contents
- [Advanced topic](#advanced-topic)
- [Table of contents](#table-of-contents)
  - [1. `...` syntax](#1--syntax)
    - [1.1. Rest parameters](#11-rest-parameters)
    - [1.2. Spread syntax](#12-spread-syntax)
    - [1.3. Summary](#13-summary)

## 1. `...` syntax

### 1.1. Rest parameters

```js
function func(a, b, ...rest) {
  console.log(a); // first argument
  console.log(b); // second argument
  console.log(rest); // the rest of argument of elements
}

func(1, 2, 3, 4, 5);
// a = 1
// b = 2
// rest = [3, 4, 5]

// sum

function sum(...numbers) {
  return numbers.reduce((total, n) => total + n, 0);
}

console.log(sum(1, 2, 3, 4)); // 10

// separate array

let [first, ...others] = [10, 20, 30, 40];
console.log(first); // 10
console.log(others); // [20, 30, 40]

// separate object

let { name, ...info } = { name: "Quý", age: 21, city: "Hà Nội" };
console.log(name); // "Quý"
console.log(info); // { age: 21, city: "Hà Nội" }
```

### 1.2. Spread syntax

```js
// rest
function printAll(...args) {
  console.log(args);
}
printAll(1, 2, 3); // [1, 2, 3]

// spread
let nums = [1, 2, 3];
printAll(...nums); // [1, 2, 3]
```

### 1.3. Summary

- `...rest`: collect into array/obj.
- `...spread`: spread into individual elements.