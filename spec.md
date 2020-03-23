Spread syntax for use with `await` keyword with optional `some` keyword
===

Stage: Draft
---

Author: Marcin Misiurski

Issue: https://github.com/tc39/proposal-async-iteration/issues/103

Synopsis
---

In this document, we propose extending existing syntax to support `await` with `some` keyword for use with spread syntax operator.

### Should
* Support default spread behaviour without any changes in code

### May not
* Break any existing syntax

*Implying [top level await](https://github.com/tc39/proposal-top-level-await)*

Current syntax
---
```js
async function* gen() {
  yield Promise.resolve(1);
  yield Promise.resolve(2);
  yield Promise.resolve(3);
}

const values = [];
const somevalues = [];
const SOME_LIMIT = 2;

let i = 0;

for await (const item of gen()) {
  values.push(item);

  if (i++ < SOME_LIMIT) {
    somevalues.push(item);
  }
}

console.log(values, somevalues);
```

Proposed syntax
---
```js
async function *gen() {
  yield Promise.resolve(1);
  yield Promise.resolve(2);
  yield Promise.resolve(3);
}

const values = [...await gen()];
const somevalues = [...await some(2) gen()];
console.log(values, somevalues);
// [ 1, 2, 3 ] [ 1, 2 ]
```