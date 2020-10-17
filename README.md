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
For example, we have 2 files in the "lib" folder: "MyClass.jsx" and "MyClass.js".  
After compilation both of these files become "MyClass.js", which can lead to errors when using this file in the code.  
It is just one of many examples...  
**Summary**: JSX is not required anymore.  
[Facebook issue](https://github.com/facebook/create-react-app/issues/87)

---

## Common JavaScript

#### New variables should contain null
All created, without any known values, new variables should contain null.  
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

#### Use destructuring in functions arguments
If function accept more than one argument use destructuring.

Benefits:

* Eliminates dependence on order of arguments
* Arguments become named

##### ❌ BAD 
```javascript
const IN_BOX = 6;
const calculatePrice = (itemPrice, count, discount = 1, balance = 0) => (
  (itemPrice * count * discount) - balance 
);

const price = calculatePrice(
  5,
  IN_BOX,
  1,
  10
);
```

##### ✔ GOOD 
```javascript
const IN_BOX = 6;
const calculatePrice = ({ itemPrice, count, discount = 1, balance = 0 }) => (
  (itemPrice * count * discount) - balance 
);

const price = calculatePrice({
    count: IN_BOX,
    itemPrice: 6,
    balance: 10,
});
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
const sum = ({ a, b }) => (a + b); // "sum" is named arrow function which has name in stacktrace
```

[When should I use Arrow functions in ECMAScript 6?](https://stackoverflow.com/questions/22939130/when-should-i-use-arrow-functions-in-ecmascript-6)

---

#### Prefer single return
It will be a single place you have to look to trace backwards and figure out what a function returns.  
Easier to debug and easier to modify.  

##### ❌ BAD
```javascript
const sayMyName = (who) => {
  if (who === 'David Guetta') {
    return `${who}: Say my name, say my name\n If you love me, let me hear you.`;
  } else if (who === 'Breaking Bad') {
    return `${who}: You all know exactly who I am. Say my name.`
  }
  return `${who}: I do not know.`;
};
```

##### ✔ GOOD 
```javascript
const sayMyName = (who) => {
  let partOfText = `${who}: I do not know.`;
  if (who === 'David Guetta') {
    partOfText = `${who}: Say my name, say my name\n If you love me, let me hear you.`;
  } else if (who === 'Breaking Bad') {
    partOfText = `${who}: You all know exactly who I am. Say my name.`
  }
  return partOfText;
};
```

[airbnb - single return vs multiple returns](https://github.com/airbnb/javascript/issues/761)

---

#### Use public class fields syntax 
Use the constructor only when necessary,  
otherwise define public properties and methods in the class body.

* Reduce amount of code
* Autobinding

##### ❌ BAD
```javascript
class Basket {
  constructor () {
    this.count = 0;
    this.handleAdd = this.handleAdd.bind(this);
  }

  handleAdd({ add }) {
    this.count += add;
  }
}
```

##### ✔ GOOD 
```javascript
class Basket {
  count = 0;

  handleAdd = ({ add }) => {
    this.count += add;
  };
}
```

[React doc - Handling events](https://reactjs.org/docs/handling-events.html)   
[React doc - Autobinding](https://reactjs.org/docs/react-without-es6.html#autobinding)

---

#### Prefer Promise 
Prefer Promise and Async functions instead of Callbacks.  
Async functions as a very powerful tool of JavaScript.   
Each Promise creates a new Microtask which can be executed in the Microtask queue of the Event Loop.   
This architecture allows split calculations on "independent" tasks and does not block the whole Event Loop.   
Callbacks in some cases can create synchronous chains that block the user interface.  

[MDN - Using microtasks in JavaScript](https://developer.mozilla.org/en-US/docs/Web/API/HTML_DOM_API/Microtask_guide)

---

#### Prefer promise.catch()
✎✎✎ to be discussed  
try/catch will be executed synchronously.  
If try{} receives an error, catch{} will execute immediately.  
In contrast to this, promise.catch() will add new Microtask in Event Loop queue.  

##### ❌ BAD
```javascript
const myAsyncFunction = async (id) => {
  let result = null;
  try {
    const partA = await getPartA(id);
    const partB = await getPartB(id);
    result = { partA, partB };
  } catch (err) { // The Catch block will be processed immediately, and not as a microtask
    logError(error);
  }

  // Obviously this is the finally part
  await logResult({ id, result });
  return result;
};
```

##### ✔ GOOD 
```javascript
const myAsyncFunction = (id) => (
  Promise.resolve()
    .then(async () => {
      const partA = await getPartA(id);
      const partB = await getPartB(id);
      return { partA, partB };
    }).catch(() => {
      logError(error);
      return null;
    }).then(async (result) => {
      await logResult({ id, result });
    })
);
```

---


Copyright © 2017 Stanislav Kochenkov 



