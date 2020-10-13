# Code Guide for Web Development in JS stack

---

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

## Files

### Separate entities by files
If your logic requires more than 400 lines of code, it's time to think about splitting it into a couple of files.
For example: move all constants to file "constants.js", move large functions to separate files, move validations.

Benefits:

* The less code the easier it is to understand it.
* Files with clear names make it easy to navigate the project.
* Separation of code into small entities makes it easier to write unit tests.
* Conflicts in small files are easier to resolve when merging into a git.
* It's easier to split code into modules.

---

### Self described file names
All files and folders should have names that describe content. 

✔ For example:

* If the file contains a list of constants which is exported, use the name "constants.js".
* If there is some helper function which is exported by default, the file should have a name like the name of this function ("someHelperToDoCalculations.js").
* File which export by default JS Class should be named as this Class with the first letter in uppercase. “MyClass.js”

❌ Don't use common words like:

* "module" (use name of this module), 
* "hoc" (use name of React class), 
* "middleware" (use type of middleware or what it do)

---

### Group files by modules and not by type
Much more often it is necessary to modify one particular module than all files with constants in the project. Therefore:

* It makes it easier to find all the files associated with the module. 
* Repeatedly simplifies the replacement/modification of structure in the module.
* Each module becomes independent, and can be implemented using a different architecture that better meets the requirements.

##### ❌ BAD
```
root
    components
        grid
        button
        input
    constants
        grid
        button
        input
    reducers
        grid
        button
        input
```

##### ✔ GOOD 
```
root
    grid
        component
        constants
        reducer
    button
        component
        constants
        reducer
    input
        component
        constants
        reducer
```

---

### Don't use file extension “.jsx”.
For example, we have 2 files in the "lib" folder: "MyClass.jsx" and "MyClass.js".<br>
After compilation both of these files become "MyClass.js", which can lead to errors when using this file in the code.<br>
It is just one of many examples...<br>
**Summary**: JSX is not required anymore.<br>
[Facebook issue](https://github.com/facebook/create-react-app/issues/87)

---

## Common JavaScript

#### New variables should contain null
All created, without any known values, new variables should contain null.<br>
This rule helps to easily distinguish non-existent properties and variables from cleaned or already created but not have value.

##### ❌ BAD
```javascript
let a;
const obj = {
    c: undefined,
};

console.log(a) // undefined
console.log(obj.c) // undefined
console.log(obj.b) // undefined
```

##### ✔ GOOD 
```javascript
let a = null;
const obj = {
    c: null,
};

console.log(a) // null
console.log(obj.c) // null
console.log(obj.b) // undefined
```

---

#### Use arrow functions 
in all cases when you don't need context of this particular function.

##### ❌ BAD
```javascript
function sum ({ a, b }) {
    return a + b;
}
```

##### ✔ GOOD 
```javascript
const sum = ({ a, b }) => (a + b);
```

[When should I use Arrow functions in ECMAScript 6?](https://stackoverflow.com/questions/22939130/when-should-i-use-arrow-functions-in-ecmascript-6)

Copyright © 2017 Stanislav Kochenkov 



