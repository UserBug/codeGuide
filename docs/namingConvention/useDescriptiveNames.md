## Naming convention - Use descriptive names

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

[Google - JS Styleguide - Naming rules common to all identifiers](https://google.github.io/styleguide/jsguide.html#naming-rules-common-to-all-identifiers)  
[Airbnb - JS Styleguide - Naming descriptive](https://github.com/airbnb/javascript#naming--descriptive)

```json
"unicorn/no-keyword-prefix": [
    "error", {
        "disallowedPrefixes": [
            "new", "for", "class", "await", "let", "var", "const", "_"
        ]
    }
]
```

[eslint-plugin-unicorn - no-keyword-prefix](https://github.com/sindresorhus/eslint-plugin-unicorn/blob/main/docs/rules/no-keyword-prefix.md)


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

---

[Back to Code Guide - Naming convention](https://github.com/UserBug/codeGuide/tree/v2/docs/namingConvention)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 