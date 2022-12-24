## Files

### Support only case sensitive path.

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
* If there is some helper function which is exported by default, the file should have a name like the name of this
  function ("someHelperToDoCalculations.js").
* File which export by default JS Class should be named as this Class with the first letter in uppercase. “MyClass.js”

❌ Don't use common words like:

* "module" (use name of this module),
* "hoc" (use name of React class),
* "middleware" (use type of middleware or what it do)

```json
"unicorn/filename-case": [
	"error",
	{
		"cases": {
			"camelCase": true,
			"pascalCase": true
		}
	}
]
```
[eslint-plugin-unicorn - filename-case](https://github.com/sindresorhus/eslint-plugin-unicorn/blob/main/docs/rules/filename-case.md)  
[eslint-plugin-unicorn - no-empty-file](https://github.com/sindresorhus/eslint-plugin-unicorn/blob/main/docs/rules/no-empty-file.md)

---

### Group files by modules and not by type - Screaming Architecture

Much more often it is necessary to modify one particular module than all files with constants in the project. Therefore:

* It makes it easier to find all the files associated with the module.
* Repeatedly simplifies the replacement/modification of structure in the module.
* Each module becomes independent, and can be implemented using a different architecture that better meets the
  requirements.

[Screaming Architecture - Uncle Bob](https://blog.cleancoder.com/uncle-bob/2011/09/30/Screaming-Architecture.html)  

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

### Separate exports

If the file contains many independent entities, export them independently.  
This will allow the collector to make the TreeShacking and reduce the size of the final file.

##### ❌ BAD

```javascript
const myFunction = () => {};
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
export const myFunction = () => {};
export const mysomeConst = 3;
export const config = {};
```

---
Copyright © 2017 Stanislav Kochenkov 
