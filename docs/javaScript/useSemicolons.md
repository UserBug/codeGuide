## JavaScript - JavaScript - Use Semicolons

When JavaScript encounters a line break without a semicolon,  
it uses a set of rules called Automatic Semicolon Insertion  
to determine whether it should regard that line break as the end of a statement,  
and (as the name implies) place a semicolon into your code before the line break if it thinks so.  
ASI contains a few eccentric behaviors, though,  
and your code will break if JavaScript misinterprets your line break.  
These rules will become more complicated as new features become a part of JavaScript.  
Explicitly terminating your statements and  
configuring your linter to catch missing semicolons will help prevent you from encountering issues.

[Airbnb - JS Styleguide - Semicolons required](https://github.com/airbnb/javascript#semicolons--required)  
[Google - JS Styleguide - Semicolons are required](https://google.github.io/styleguide/jsguide.html#formatting-semicolons-are-required)  

##### ❌ BAD

```javascript
// Raises exception
const luke = {}
const leia = {}
    [luke, leia].forEach((jedi) => jedi.father = 'vader')

const reaction = "No! That’s impossible!"
(async function meanwhileOnTheFalcon() {
    // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
    // ...
}())

// Returns `undefined` instead of the value on the next line - always happens when `return` is on a line by itself because of ASI!
function foo() {
    return
    'search your feelings, you know it to be foo'
}
```

##### ✔ GOOD

```javascript
const luke = {};
const leia = {};
[luke, leia].forEach((jedi) => {
    jedi.father = 'vader';
});

const reaction = "No! That’s impossible!";
(async function meanwhileOnTheFalcon() {
    // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
    // ...
}());

function foo() {
    return 'search your feelings, you know it to be foo';
};
```

---

[Back to Code Guide - JavaScript](https://github.com/UserBug/codeGuide/tree/v2/docs/javaScript)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 