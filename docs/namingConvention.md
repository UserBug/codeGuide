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

### TODO template
Each TODO comment must include additional information:  
Full name of the author and ID of the ticket in which this comment is planned to be corrected.
Why is it important?
* TODO comments are created for cases when correction is needed,  
  but these changes are blocked or strongly affect the duration of the task.
* In most cases, a couple of sentences of text in a commentary is not enough to save and transfer the entire context of the issue that needs to be corrected,  
  and the author of the commentary is the best carrier of such information.  
  Having a name allows you to immediately recognize the best person who should be contacted for all questions.
* As a result of many actions in Git, the history of file changes can be lost or overwritten,  
  in which case it will not reflect the real author of TODO comment.  
  Therefore, it is important to manually save its name.
* The ticket ID serves as a trigger for action.  
  If a comment does not have a ticket ID attached, it is unclear when and by whom it will be corrected,  
  which means it will most likely be forgotten.

##### ❌ BAD
```javascript
const a = 1; // TODO Change variable name
```

##### ✔ GOOD
```javascript
const a = 1; // TODO - Alan Smithee - Change variable name - JIRA-1111
```

---
Copyright © 2017 Stanislav Kochenkov
