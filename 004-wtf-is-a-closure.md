# WTF is a Javascript Closure

Another one of those confusing topics that we never spend enough time nailing it down.

## TL;DR

We talk of **closure** when an inner function has access to the variables/parameters of its outer function, even after the outer function has returned.


## Closures

Javascript variables can belong to the **local** or **global** scope. Global variables can be made local (private) using **closures**.

Javascript supports the creation of **nested functions**. A nested function has access to the variables and parameters of its outer function even when the outer function has returned. The inner function is called a **closure**, as it closes on the variables and parameters of the lexical scope where it is implemented. A couple of very simple examples below.

```js
function outerFunc() {
  let outerVar = 100;

  return function innerFunc() {
    console.log("logged:", outerVar);
  };
}

const closure = outerFunc();
closure(); // logged: 100
```

```js
function outerFunc(outerParam) {
  return function innerFunc() {
    console.log("logged:", outerParam);
  };
}

const closure = outerFunc(59);
closure(); // logged: 59
```

## Let's build a Counter

Let's assume we want to be able to count something, it does not matter what. What you want though, is that the value of **counter** is made available to all functions. Let's explore a few options to build up to closures and (hopefully) understand their value.

### Option #1 - using a global variable

You could use a global variable and build a simple function to increase the value of that variable. 

As you can see below though, this is not a good solution. The variable counter can be manually modified and it is therefore **not** a reliable way to build our counter.

```js
let counter = 0; // global variable

function plus() {
  counter += 1;
  console.log("counter:", counter);
}

plus(); // counter: 1
plus(); // counter: 2
plus(); // counter: 3

counter = 59; // not great!
plus(); // counter: 60
```

### Option #2 - using a local variable

Exchanging the global counter variable with a local counter variable and accessing the local counter variable by letting the function return it could be a step in the right direction. Unfortunately, doing that, we actually broke the `plus()` function.

Local variables are "destroyed" when their functions are returned and, every time `plus()` is called, a new counter variable is declared and initialised to `0`. That is why we always get value `1` in the console.

```js
function plus() {
  let counter = 0;
  counter += 1;
  return counter;
}

console.log("counter:", plus()); // counter: 1
console.log("counter:", plus()); // counter: 1
console.log("counter:", plus()); // counter: 1
```

### Option #3 - using an inner function

Above, we explored two options:

- the first works but it is unreliable; and
- the second, even if it could be considered a step in the right direction, it does not work at all.

We need to find a way to maintain the state of the local variable. Inner functions help us do just that.

```js
function plus() {
  let counter = 0;
  const addOne = () => (counter += 1);
  addOne();
  return counter;
}

console.log("counter:", plus()); // counter: 1
console.log("counter:", plus()); // counter: 1
console.log("counter:", plus()); // counter: 1
```

This first attempt, unfortunately, does not help us solve our issue as we still have the issue of executing `let counter = 0;` every time we call `plus()`.

What we need is, surprise surprise, a **closure**.

Instead of returning _counter_ directly, we return the inner function (what before was the `add()` function) that has access to _counter_ and it will still have access to _counter_ even after `plus()` has returned.

```js
function plus() {
  let counter = 0;
  function addOne() {
    return (counter += 1);
  }
  return addOne;
}

const add = plus(); // "add" is now a closure

console.log("counter:", add()); // counter: 1
console.log("counter:", add()); // counter: 2
console.log("counter:", add()); // counter: 3
```

The outer function `plus()` is called only once and it returns a function expression assigned to the variable `add`.

`add` is what, in Javascript, we call a **closure**. A function that can access the `counter` variable in the parent lexical scope, even after the parent function has closed.

> We say that `addOne` closes over the `counter` variable (not its value!).

The `counter` variable has now being transformed into a **private** variable. Its state is protected and it cannot be tempered with, but by calling the `add` function expression.

> NOTE: A function which is assigned to a variable is called a **function expression**.

> NOTE: Closures are created every time a function is created, at function creation time.

Extra: below another implementation of counter, slightly different but using the same concepts. `createAdderFunc` is a _function factory_ as it allow the programmer to build many different functions on top of it.

```js
function createAdderFunc(num) {
  return (val) => val + num;
}
const addOne = createAdderFunc(1);
const addTwentyTwo = createAdderFunc(22);
console.log(addOne(55)); // 56 (= 55 + 1)
console.log(addTwentyTwo(3)); // 25 (= 3 + 22)
```

Extra: below (yet) another implementation of counter, a more complete version of it.

```js
function makeCompleteCounter() {
  let privateCounter = 0;
  const changeBy = (val) => (privateCounter += val);

  return {
    // all the below functions are closures sharing the same lexical scope
    // that contains two private items: privateCounter and changeBy.
    plusOne: () => console.log(changeBy(1)),
    minusOne: () => console.log(changeBy(-1)),
    getValue: () => console.log(privateCounter),
    reset: () => console.log((privateCounter = 0)),
  };
}

const counter = makeCompleteCounter();

counter.getValue(); // 0
counter.plusOne(); // 1
counter.plusOne(); // 2
counter.minusOne(); // 1
counter.getValue(); // 1
counter.reset(); // 0
counter.minusOne(); // -1
```

## Closure scope chain

It may not be immediately obvious, but the depth to which closures can go is theoretically infinite. As per the definition, any inner function would be considered a closure to the outer scope variables or parameters. As such, the inner function of an inner function would be a closure itself.

```js
const deepSum = function (a) {
  let sum = 0;
  return function (b) {
    return function (c) {
      return function (d) {
        return sum + a + b + c + d;
      };
    };
  };
};

console.log(deepSum(1)(2)(3)(4)); // 10
```

You do not need to use anonymous functions... see below.

```js
function deepSum(a) {
  let sum = 0;
  return function firstSum(b) {
    return function secondSum(c) {
      return function thirdSum(d) {
        return sum + a + b + c + d;
      };
    };
  };
}

console.log(deepSum(1)(2)(3)(4)); // 10
```

## Why use closures?

Closures are useful in hiding implementation details (abstraction) and garanteeing that variables or inner functions remain private (encapsulation).

This behaviour may remind you of Object Oriented Programming (OOP), where objects' properties (variables) are associated with objects' methods (inner functions). Closures can therefore be utilised anytime you would have normally used an object with a single method.
