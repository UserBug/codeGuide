## Naming convention - JavaScript Classes

All definitions of JS Classes should use PascalCase.

[Google - JS Styleguide - Naming local variable names](https://google.github.io/styleguide/jsguide.html#naming-local-variable-names)  
[Airbnb - JS Styleguide - PascalCase](https://github.com/airbnb/javascript#naming--PascalCase)


##### ❌ BAD

```javascript
class myClass {};
class MY_CLASS {};
const myClass = () => { /* constructor as function*/ };
const SOME_CALCULATED_DATA = calculateData();
```

##### ✔ GOOD

```javascript
class MyClass {
};
const MyClass = () => { /* constructor as function*/
};
const FREEZE_OBJECT = Object.freeze({})
const notFreezeObject = {};
const someCalculatedData = calculateData();
```

---

[Back to Code Guide - Naming convention](https://github.com/UserBug/codeGuide/tree/v2/docs/namingConvention)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 