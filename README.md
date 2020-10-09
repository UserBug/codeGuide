# Code Guide for Web Development in JS stack


## Naming convention

### Variables, functions, CSS classes
should use CamelCase naming with lowercase first letter.
##### :x: BAD
```javascript
var MySomeVar = 3;
let mysomeVar = 3;
const MY_SOME_FUNCTION = () => {};
```
```css
.someCSSClass {}
```

##### :heavy_check_mark: GOOD 
```javascript
let mySomeVar = 3;
const mySomeFunction = () => {};
```
```css
.someCssClass {}
```

---

### JS Classes
All definitions of JS Classes should use CamelCase naming with uppercase first letter.
##### :x: BAD
```javascript
class myClass {};
class MY_CLASS {};
const myClass = () => { /* constructor as function*/ };
```

##### :heavy_check_mark: GOOD 
```javascript
class MyClass {};
const MyClass = () => { /* constructor as function*/ };
```

---

Copyright © 2017 Stanislav Kochenkov 



