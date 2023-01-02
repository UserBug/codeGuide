## JavaScript - New variables should contain null

All created, without any known values, new variables should contain null.  
This rule helps to easily distinguish non-existent properties and variables from cleaned or already created but not have
value.

Object.prototype.hasOwnProperty() cannot be conveniently applied to large objects.

It also helps maintain consistency with the server side.  
In queries "undefined" and "null" have different meanings:

- "undefined" - Value not set
- "null" - The value is set as void

[MDN Web Docs - null](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/null)  
[eslint - init-declarations](https://eslint.org/docs/rules/init-declarations)

Combination of:  
[eslint - no-undefined](https://eslint.org/docs/latest/rules/no-undefined)  
[eslint - no-undef-init](https://eslint.org/docs/latest/rules/no-undef-init)

##### ❌ BAD

```javascript
let a;
const obj = {
    c: undefined,
};

console.log(a) // undefined
console.log(b) // undefined
console.log(obj.c) // undefined
console.log(obj.d) // undefined
```

##### ✔ GOOD

```javascript
let a = null;
const obj = {
    c: null,
};

console.log(a); // null
console.log(b); // undefined
console.log(obj.c); // null
console.log(obj.d); // undefined
```

---

[Back to Code Guide - JavaScript](https://github.com/UserBug/codeGuide/tree/v2/docs/javaScript)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 