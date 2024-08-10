Question 1:

```
let a = {};
let b = { key: 'b' };
let c = { key: 'c' };

a[b] = 123;
a[c] = 456;

console.log(a[b]);

```

This will output :<b>456</b>
<b>Explanation :</b>
Objects in JavaScript use keys as strings for property names. When b and c are used as keys in a, they are converted to the string `[object Object].` This causes both `a[b]` and `a[c]` to reference the same property, so the value is overwritten when `a[c] = 456` is executed. Hence, `console.log(a[b])` outputs `456.`

Question 2:

```
let count = 0;
(function immediate() {
  if (count === 0) {
    let count = 1;
    console.log(count);
  }
  console.log(count);
})();

```

This will output :<b> 1 undefined</b>
<b>Explanation :</b>
The let keyword creates a new block-scoped variable count inside the if statement, shadowing the outer count. The first console.log(count) prints 1, and the second console.log(count) prints undefined because the block-scoped count variable is not accessible outside the if statement.

Question 3:

```
let x = [1, 2, 3];
let y = x;
y.push(4);

console.log(x);
console.log(y);

```

This will output :<b>[1, 2, 3, 4] and [1,2,3,4]</b>
<b>Explanation :</b>
In JavaScript, arrays are reference types. When y is assigned to x, both y and x refer to the same array. Modifying y also affects x, so both x and y contain [1, 2, 3, 4].

Question 4:

```
function foo() {
  var bar = "bar";

  setTimeout(function() {
    console.log(bar);
  }, 1000);

  console.log("foo");
}

foo();

```

This will output :<b>foo bar</b>
<b>Explanation :</b>
The setTimeout function is asynchronous and will run after `foo()` finishes executing. First, `"foo"` is logged, and then after 1 second, `"bar"` is logged.

Question 5:

```
console.log(0.1 + 0.2 == 0.3);
```

This will output :<b>false</b>
<b>Explanation :</b>
Due to `floating-point` `precision` errors in JavaScript, `0.1 + 0.2` does not `exactly` equal `0.3`; it is slightly more, resulting in false.

Question 6:

```
console.log(typeof null);
```

This will output :<b>object</b>
<b>Explanation :</b>
The typeof operator in JavaScript returns `"object"` for `null`, which is a known `quirk` of the language. This is due to how `null` is represented at the low level in JavaScript.

Question 7:

```
function createCounter() {
  let count = 0;
  return function() {
    count++;
    return count;
  };
}

const counter = createCounter();
console.log(counter());
console.log(counter());

```

This will output :<b>1 2</b>
<b>Explanation :</b>
The createCounter function returns a closure that retains access to the count variable. Each time the counter function is called, count is incremented and returned, resulting in 1 and 2 being printed.

Question 8:

```
const obj = {
  value: 1,
  increment: function() {
    this.value++;
  }
};

const increment = obj.increment;
increment();
console.log(obj.value);

```

This will output :<b>1</b>
<b>Explanation :</b>
When the increment method is assigned to a new variable, it `loses` its context `(this),` which would usually point to obj. Here, this.value is `undefined`, so obj.value remains unchanged.

Question 9:

```
const promise = new Promise((resolve, reject) => {
  setTimeout(() => resolve('Resolved!'), 1000);
});

promise.then(response => {
  console.log(response);
});

console.log('Start');
```

This will output :<b>Start Resolved!</b>
<b>Explanation :</b>
The promise is asynchronous, so `"Start"` is logged first, followed by `"Resolved!"` after 1 second.

Question 10:
```
const numbers = [1, 2, 3, 4, 5];
const result = numbers.map(n => n * 2).filter(n => n > 5);
console.log(result);
```
This will output :<b>[6,7,10]</b>
<b>Explanation :</b>
The map function multiplies each element by 2, resulting in `[2, 4, 6, 8, 10].` The filter function then removes numbers 5 or below, leaving `[6, 8, 10].`

Question 11:
```
const obj = {
  value: 10,
  getValue: function() {
    return this.value;
  }
};

const getValue = obj.getValue;
console.log(getValue());
```
This will output :<b>Undifined</b>
<b>Explanation :</b>
Similar to question 8, `getValue` loses its `context` (this) when assigned to a variable, resulting in this.value being `undefined.`
