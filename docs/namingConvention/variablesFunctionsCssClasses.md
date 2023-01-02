## Naming convention - Variables, functions, CSS classes

Variables, functions, CSS classes should use CamelCase naming with lowercase first letter.

[Google - JS Styleguide - Naming local variable names](https://google.github.io/styleguide/jsguide.html#naming-local-variable-names)  
[Mozilla - JS Styleguide - Variable naming](https://developer.mozilla.org/en-US/docs/MDN/Guidelines/Code_guidelines/JavaScript#variable_naming)

##### ❌ BAD

```javascript
var MySomeVar = 3;
let mysomeVar = 3;
const MY_SOME_FUNCTION = () => {};
```

```css
.someCSSClass {}
```

##### ✔ GOOD

```javascript
let mySomeVar = 3;
const mySomeFunction = () => {};
```

```css
.someCssClass {}
```

---

[Back to Code Guide - Naming convention](https://github.com/UserBug/codeGuide/tree/v2/docs/namingConvention)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 