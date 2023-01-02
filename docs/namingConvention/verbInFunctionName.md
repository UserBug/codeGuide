## Naming convention - Verb in Function name

Name of all methods and functions must contain a Verb.  
Since any function performs an action, it must explicitly reflect this in the name.  
This will allow you to easily distinguish it in the code and improve your understanding of its purpose.

[Google - JS Styleguide - Naming method names](https://google.github.io/styleguide/jsguide.html#naming-method-names)  

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

---

[Back to Code Guide - Naming convention](https://github.com/UserBug/codeGuide/tree/v2/docs/namingConvention)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 