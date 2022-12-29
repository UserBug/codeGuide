## Separate exports

If the file contains many independent entities, export them independently.  
This will allow the collector to make the TreeShacking and reduce the size of the final file.

##### ❌ BAD

```javascript
const myFunction = () => {
};
const mysomeConst = 3;
const config = {};

export default {
    myFunction,
    mysomeConst,
    config,
};
```

##### ✔ GOOD

```javascript
export const myFunction = () => {
};
export const mysomeConst = 3;
export const config = {};
```

---

[Back to Code Guide - Files](https://github.com/UserBug/codeGuide/tree/v2/docs/files)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 