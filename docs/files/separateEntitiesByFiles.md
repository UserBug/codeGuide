## Separate entities by files

If your logic requires more than 400 lines of code, it's time to think about splitting it into a couple of files.
For example: move all constants to file "constants.js", move large functions to separate files, move validations.

Benefits:

* The less code the easier it is to understand it.
* Files with clear names make it easy to navigate the project.
* Separation of code into small entities makes it easier to write unit tests.
* Conflicts in small files are easier to resolve when merging into a git.
* It's easier to split code into modules.

Related: [Code Guide - Split Code - Shorten Files](https://github.com/UserBug/codeGuide/blob/v2/docs/splitCode/shortenFiles.md)  

---

[Back to CodeGuide - Files](https://github.com/UserBug/codeGuide/tree/v2/docs/files)

[Back to CodeGuide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 