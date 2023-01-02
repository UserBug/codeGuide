## Styles - Use css variables

If the requirements of your project allow you to use pure css constants - do it.  
This will allow you to:

* Store style constants in one place
* Change styles dynamically with css

[mozilla - CSS variables Browser compatibility](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties#Browser_compatibility)

```scss
// theme/colors.scss
:root {
  --PRIMARY_DARK_COLOR: #213943;
  --PRIMARY_LIGHT_COLOR: #78909c;
  --PRIMARY_VERY_LIGHT_COLOR: #a7c0cd;
}

$PRIMARY_DARK_COLOR: var(--PRIMARY_DARK_COLOR);
$PRIMARY_LIGHT_COLOR: var(--PRIMARY_LIGHT_COLOR);
$PRIMARY_VERY_LIGHT_COLOR: var(--PRIMARY_VERY_LIGHT_COLOR);
```

---

[Back to Code Guide - Styles](https://github.com/UserBug/codeGuide/tree/v2/docs/styles)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 