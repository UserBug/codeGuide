## Naming convention

### Variables, functions, CSS classes
should use CamelCase naming with lowercase first letter.
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

### JS Classes
All definitions of JS Classes should use CamelCase naming with uppercase first letter.
##### ❌ BAD
```javascript
class myClass {};
class MY_CLASS {};
const myClass = () => { /* constructor as function*/ };
```

##### ✔ GOOD
```javascript
class MyClass {};
const MyClass = () => { /* constructor as function*/ };
```

---

### Constants
All constants should use Snake case naming with all letters in uppercase.

##### ❌ BAD
```javascript
const MySomeConst = 3;
const mysomeConst = 'a';
const MY_SOME_CONST = () => {};
```

##### ✔ GOOD
```javascript
const MY_SOME_CONST = 3;
const mySomeConst = () => {};
```

---

### URL
All URL paths should use the kebab case in lowercase.

##### ❌ BAD
```
www.site.com/MyURLPath
www.site.com/MY-URL
www.site.com/my_url
```

##### ✔ GOOD
```
www.site.com/my-url
```

---
