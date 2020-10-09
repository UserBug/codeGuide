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

### Constants
All constants should use Snake case naming with all letters in uppercase.

##### :x: BAD
```javascript
const MySomeConst = 3;
const mysomeConst = 'a';
const MY_SOME_CONST = () => {};
```

##### :heavy_check_mark: GOOD 
```javascript
const MY_SOME_CONST = 3;
const mySomeConst = () => {};
```

---

### URL 
All URL paths should use the kebab case in lowercase.

##### :x: BAD
```
www.site.com/MyURLPath
www.site.com/MY-URL
www.site.com/my_url
```

##### :heavy_check_mark: GOOD 
```
www.site.com/my-url
```

---

### URL 
All URL paths should use the kebab case in lowercase.

##### :x: BAD
```
www.site.com/MyURLPath
www.site.com/MY-URL
www.site.com/my_url
```

##### :heavy_check_mark: GOOD 
```
www.site.com/my-url
```

---

Copyright © 2017 Stanislav Kochenkov 



