## Styles - Prefer class agents child selectors

Long tag selectors tie styles to the structure of components.  
The hierarchy of elements within a component can change frequently,  
which immediately breaks styles.  
To prevent this, create and use more class names.

##### ❌ BAD

```scss
.myComponent > div > div {}
```

##### ✔ GOOD

```scss
.myComponent .header {}
```

---

[Back to Code Guide - Styles](https://github.com/UserBug/codeGuide/tree/v2/docs/styles)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 