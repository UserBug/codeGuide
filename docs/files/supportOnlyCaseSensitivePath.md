## Files - Support only case-sensitive path

According to the naming convention, register is an extremely important part of the name.  
For example, "User" is a class, and "user" is an instance of the class "User."

```javascript
// Two absolutely correct imports that can exist in one file.
import Documents from './components/Documents';
import documents from './components/documents';
```

The lack of sensitivity to the register leads to uncertainty of imports  
and the inability to correctly support the launch of projects on Unix.

---

[Back to Code Guide - Files](https://github.com/UserBug/codeGuide/tree/v2/docs/files)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 