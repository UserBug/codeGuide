## JavaScript - Avoid nested destruction

Retrieving a value from a deep level of an object using destructuring syntax  
has a number of undesirable consequences:

* Finding the paths used to get values from Objects in a project is very difficult.
* Creation of scripts for analyzing and modifying the codebase is difficult.

##### ❌ BAD

```javascript
import someVeryLargeAndMultilevelObject from 'strangeObjectsCollection';

const {varFromLevel1: {varFromLevel2: {varFromLevel3: {varFromLevel4}}}} = someVeryLargeAndMultilevelObject;

const myObj = {varFromLevel1: {varFromLevel2: 111}};
```

##### ✔ GOOD

```javascript
import someVeryLargeAndMultilevelObject from 'strangeObjectsCollection';

const varFromLevel4 = someVeryLargeAndMultilevelObject.varFromLevel1.varFromLevel2.varFromLevel3.varFromLevel4;
```
  
---

[Back to CodeGuide - JavaScript](https://github.com/UserBug/codeGuide/tree/v2/docs/javaScript)  
  
[Back to CodeGuide - Readme](https://github.com/UserBug/codeGuide/tree/v2)  

---
Copyright © 2017 Stanislav Kochenkov 