1
```
function sayHi() {
  console.log(name);
  console.log(age);
  var name = 'Lydia';
  let age = 21;
}

sayHi();
```
This will output: <b>Undefined and referance error</b>

<b>Explanation : </b>
Within the function, the `name` variable is declared with the var keyword, which means it gets `hoisted` with the default value of undefined until the line where it is defined. At the time we log name, it holds the value undefined. Variables declared with the `let` keyword are also hoisted, but are not initialized and are in a `"temporal dead zone"` until their declaration is encountered. Trying to access age before its declaration results in a `ReferenceError.`

2

```
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1);
}

for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1);
}

```
This will output: <b>3 3 3 and 0 1 2</b>

<b>Explanation : </b>
Due to JavaScript's `event queue`, the setTimeout callback function is called `after` the loop has been executed. In the first loop, `i` is declared with `var` and thus is global. By the time the callback is invoked, `i` equals `3`. In the second loop, `i` is declared with `let`, making it block-scoped. Each iteration has a new `i`, so it logs `0`, `1`, and `2`.

3
```
const shape = {
  radius: 10,
  diameter() {
    return this.radius * 2;
  },
  perimeter: () => 2 * Math.PI * this.radius,
};

console.log(shape.diameter());
console.log(shape.perimeter());
```
This will output: <b>20 and NaN</b>
<b>Explanation : </b>
The diameter method is a regular function, so this refers to the shape `object`. The perimeter method is an `arrow` function, so this refers to its `surrounding` scope, not the shape object. Since this.radius is undefined in the surrounding scope, it returns `NaN`.


4
```
const bird = {
  size: 'small',
};

const mouse = {
  name: 'Mickey',
  small: true,
};
```
This will output: <b>ReferenceError: Cannot access 'bird' before initialization</b>
<b>Explanation : </b>
In JavaScript, object keys are strings. Using `bracket notation`, `mouse[bird.size]` evaluates `bird.size` first, which is `"small"`. Hence, `mouse["small"]` returns true. Using `dot` notation, mouse.bird is `undefined` since mouse does not have a bird key. Trying to access size on `undefined` throws an error.

5
```
let c = { greeting: 'Hey!' };
let d;

d = c;
c.greeting = 'Hello';
console.log(d.greeting);
```
This will output: <b>Hello</b>
<b>Explanation : </b>
In JavaScript, objects `interact` by `reference.` When d is assigned c, they `reference` the same object. Changing the object through c also changes it for d. Thus, d.greeting logs "Hello".

6
```
let a = 3;
let b = new Number(3);
let c = 3;

console.log(a == b);
console.log(a === b);
console.log(b === c);
```
This will output :<b>true, false, false</b>
<b>Explanation</b>
new Number() creates an object, not a primitive number. Using `==`, JavaScript checks only for value `equality`, so `a == b` is true. Using `===`, JavaScript checks for both value and type equality. Since b is an object and a is a number, a `===` b and `b === c` are false.

7
```
class Chameleon {
  static colorChange(newColor) {
    this.newColor = newColor;
    return this.newColor;
  }

  constructor({ newColor = 'green' } = {}) {
    this.newColor = newColor;
  }
}

const freddie = new Chameleon({ newColor: 'purple' });
console.log(freddie.colorChange('orange'));
```
This will output :<b>Referance Error</b>
<b>Explanation : </b>
The colorChange function is `static` and `belongs` to the class, not to `instances` of the `class.` Since freddie is an instance of `Chameleon`, calling `colorChange` on it throws a `TypeError.`

8
```
function sum(a, b) {
  return a + b;
}

sum(1, '2');
```
This will output :<b>12</b>
<b>Explanation : </b>
JavaScript is a dynamically typed language and performs implicit type coercion. When adding a number and a string, the number is converted to a string. Therefore, 1 + '2' results in "12".

9
```
let number = 0;
console.log(number++);
console.log(++number);
console.log(number);
```
This will output :<b>0, 2, 2</b>
<b>Explanation :</b>
The postfix ++ operator returns the value before incrementing, so number++ logs 0 and then increments to 1. The prefix ++ operator increments the value first and then returns it, so ++number logs 2. The final number value is 2.

10

```
function checkAge(data) {
  if (data === { age: 18 }) {
    console.log('You are an adult!');
  } else if (data == { age: 18 }) {
    console.log('You are still an adult.');
  } else {
    console.log(`Hmm.. You don't have an age I guess`);
  }
}

checkAge({ age: 18 });
```
This will output :<b>Hmm.. You don't have an age I guess</b>
<b>Explanation :</b>
When testing equality, primitives are compared by value, while objects are compared by reference. The objects being compared here do not reference the same location in memory, so both `{ age: 18 } === { age: 18 } and { age: 18 } == { age: 18 }` return false.

11
```
function getAge(...args) {
  console.log(typeof args);
}

getAge(21);
```
This will output :<b>object</b>
<b>Explanation :</b>
The rest parameter `...args` collects all arguments into an array. An array is an object in JavaScript, so typeof `args` returns `"object"`.

12
```
const sum = eval('10*10+5');
console.log(sum);
```
This will output :<b>105</b>
<b>Explanation :</b>
Explanation:eval evaluates a string as JavaScript code. The expression `10*10+5` is evaluated to 105.

13
```
sessionStorage.setItem('cool_secret', 123);
```
This will output :<b>When the user closes the tab.</b>

<b>Explanation :</b>
Data stored in sessionStorage is removed when the tab is closed. If localStorage was used, the data would persist until explicitly cleared.

14
```
for (let i = 1; i < 5; i++) {
  if (i === 3) continue;
  console.log(i);
}
```
This will output :<b>1, 2, 4</b>
<b>Explanation :</b>
The continue statement skips the current iteration when i equals 3, so 3 is not logged. The loop continues with the next iteration.
15
```
const obj = {
  value: 42,
  getValue: () => {
    return this.value;
  }
};

console.log(obj.getValue());
```
This will output :<b>undefined</b>
<b>Explanation :</b>
Arrow functions do not have their own this context; they inherit this from their surrounding scope. In this case, the surrounding scope is the global context, where this.value is undefined. Therefore, obj.getValue() returns undefined.





