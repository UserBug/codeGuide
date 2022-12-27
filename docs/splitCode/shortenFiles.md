### Split Code - Shorten Files

Imagine a project in which all the source code is compiled into one file of 25,000 lines.  
This will make it very difficult:

* Understand the logic
* Administer the dependencies
* Identify exit points
* Independently work as a multi-developer and do PR reviews

The number of lines of code can serve as a trigger for the need to split a file.  
It is recommended to shorten files to a maximum length of 250 lines.  
You can choose the number that best suits your project, but the number must be hard-defined.

To do this, you can turn larger files into folders,  
moving all independent functions into new small files.

There is no minimum file size limit.
A file with one function on one line of code is fine.

[Eric Raymond's "The Art Of Unix Programming" - Encapsulation and Optimal Module Size:](http://catb.org/esr/writings/taoup/html/ch04s01.html)  
_In nonmathematical terms, Hatton's empirical results imply a sweet spot between 200 and 400 logical lines of code  
that minimizes probable defect density, all other factors (such as programmer skill) being equal.  
This size is independent of the language being used — an observation which strongly reinforces the advice  
given elsewhere in this book to program with the most powerful languages and tools you can.  
Beware of taking these numbers too literally however.  
Methods for counting lines of code vary considerably according to what the analyst considers a logical line,  
and other biases (such as whether comments are stripped).  
Hatton himself suggests as a rule of thumb a 2x conversion between logical and physical lines,  
suggesting an optimal range of 400–800 physical lines._

[Rule of 30 – When is a Method, Class or Subsystem Too Big](https://levelup.gitconnected.com/javascript-code-styling-best-practices-maximum-depth-and-lines-e89bd591186c)

`max-lines: ["error", 250]`  
[eslint - max-lines](https://eslint.org/docs/latest/rules/max-lines)

##### ❌ BAD

```javascript
// File: processDataForPost.js
const getDataFromApi = (id) => { /* ... */
};
const saveDataToDb = (data) => { /* ... */
};
const formatResponce = (data) => { /* ... */
};

const processDataForPost = async (id) => {
    const data = await getDataFromApi(id);
    await saveDataToDb(data);
    return formatResponce(data);
};

// More then 250 lines
export default processDataForPost;
```

##### ✔ GOOD

```javascript
// File: processDataForPost/index.js
import getDataFromApi from './getDataFromApi.js';
import formatResponce from './formatResponce.js';
import saveDataToDb from './saveDataToDb.js';

const processDataForPost = async (id) => {
    const data = await getDataFromApi(id);
    await saveDataToDb(data);
    return formatResponce(data);
};

export default processDataForPost;
```

##### ❌ BAD

```javascript
// File: utils.js
export const cloneDeep = (obj) => { /* ... */
};
export const toCamelCase = (str) => { /* ... */
};
export const toCapitalize = (str) => { /* ... */
};
// More then 250 lines
```

##### ✔ GOOD

```javascript
// File: utils/index.js
import cloneDeep from './cloneDeep.js';
import toCamelCase from './toCamelCase.js';
import toCapitalize from './toCapitalize.js';

export {
    cloneDeep,
    toCamelCase,
    toCapitalize
};
```

[Back to CodeGuide - Split Code](https://github.com/UserBug/codeGuide/tree/v2/docs/splitCode/index.md)

[Back to CodeGuide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 