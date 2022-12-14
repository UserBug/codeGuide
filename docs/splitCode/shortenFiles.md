### Split Code - Shorten Files
Imagine a project in which all the source code is compiled into one file of 25,000 lines.  
This will make it very difficult:
* Understand the logic
* Administer the dependencies
* Identify exit points
* Independently work as a multi-developer and do PR reviews

The number of lines of code can serve as a trigger for the need to split a file.  
It is recommended to shorten files to a maximum length of 250 lines.  

To do this, you can turn larger files into folders,  
moving all independent functions into new small files.

There is no minimum file size limit.
A file with one function on one line of code is fine.

`max-nested-callbacks: ["error", 250]`  
[eslint - max-lines](https://eslint.org/docs/latest/rules/max-lines)  

##### ❌ BAD
```javascript
// File: processDataForPost.js
const getDataFromApi = (id) => { /* ... */ };
const saveDataToDb = (data) => { /* ... */ };
const formatResponce = (data) => { /* ... */ };

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
export const cloneDeep = (obj) => { /* ... */ };
export const toCamelCase = (str) => { /* ... */ };
export const toCapitalize = (str) => { /* ... */ };
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