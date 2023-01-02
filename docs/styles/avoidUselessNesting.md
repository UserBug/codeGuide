## Styles - Avoid useless nesting

##### ❌ BAD

```scss
.myComponent {
    & > .focused {

    }
}
```

##### ✔ GOOD

```scss
myComponent .focused {

}
```

---

[Back to Code Guide - Styles](https://github.com/UserBug/codeGuide/tree/v2/docs/styles)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 