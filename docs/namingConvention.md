## Naming convention

### Names says whats inside
Name of:
* Variable
* Constant
* Function
* Argument
* Class
* CssClass

Give as descriptive a name as possible, within reason.  
Do not worry about saving horizontal space  
as it is far more important to make your code immediately understandable by a new reader.  
Do not use abbreviations that are ambiguous or unfamiliar to readers outside your project,  
and do not abbreviate by deleting letters within a word.

##### ❌ BAD
```javascript
let a = 2;
const str = 'Mark';
const fn = (e) => {};
const cb = (e) => {};
const obj = {};
const BBCC = [];
```
```css
.l {}
```

##### ✔ GOOD
```javascript
let maxAllowedAnswersInForm = 1;
const userShortNameInTitle = 'Mark';
const submitButtonOnClick = (event) => {};
const sendFormDataOnError = (error) => {};
const userDataObject = {};
const userIdsArray = [];
```
```css
.defaultLinkViewForArticles {}
```

[Google - JS Styleguide - Naming rules common to all identifiers](https://google.github.io/styleguide/jsguide.html#naming-rules-common-to-all-identifiers)  
[Airbnb - JS Styleguide - Naming descriptive](https://github.com/airbnb/javascript#naming--descriptive)  

---

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

[Google - JS Styleguide - Naming local variable names](https://google.github.io/styleguide/jsguide.html#naming-local-variable-names)  
[Mozilla - JS Styleguide - Variable naming](https://developer.mozilla.org/en-US/docs/MDN/Guidelines/Code_guidelines/JavaScript#variable_naming)  

---

### JS Classes
All definitions of JS Classes should use PascalCase.
##### ❌ BAD
```javascript
class myClass {};
class MY_CLASS {};
const myClass = () => { /* constructor as function*/ };
const SOME_CALCULATED_DATA = calculateData();
```

##### ✔ GOOD
```javascript
class MyClass {};
const MyClass = () => { /* constructor as function*/ };
const FREEZE_OBJECT = Object.freeze({ })
const notFreezeObject = {};
const someCalculatedData = calculateData();
```

[Google - JS Styleguide - Naming local variable names](https://google.github.io/styleguide/jsguide.html#naming-local-variable-names)  
[Airbnb - JS Styleguide - PascalCase](https://github.com/airbnb/javascript#naming--PascalCase)

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

[Google - JS Styleguide - Naming constant names](https://google.github.io/styleguide/jsguide.html#naming-constant-names)  
[Airbnb - JS Styleguide - Naming uppercase](https://github.com/airbnb/javascript#naming--uppercase)  

---

### Verb in Function name
Name of all methods and functions must contain a Verb.  
Since any function performs an action, it must explicitly reflect this in the name.  
This will allow you to easily distinguish it in the code and improve your understanding of its purpose.  

##### ❌ BAD
```javascript
const click = () => {};
const user = () => {};
const validForm = () => {};
```

##### ✔ GOOD
```javascript
const onClick = () => {};
const saveUser = () => {};
const isFormValid = () => {};
```

[Google - JS Styleguide - Naming method names](https://google.github.io/styleguide/jsguide.html#naming-method-names)  

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
