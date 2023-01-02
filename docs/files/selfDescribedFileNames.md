## Files - Self described file names

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

[eslint-plugin-unicorn - filename-case](https://github.com/sindresorhus/eslint-plugin-unicorn/blob/main/docs/rules/filename-case.md)  
[eslint-plugin-unicorn - no-empty-file](https://github.com/sindresorhus/eslint-plugin-unicorn/blob/main/docs/rules/no-empty-file.md)

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

---

[Back to Code Guide - Files](https://github.com/UserBug/codeGuide/tree/v2/docs/files)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 