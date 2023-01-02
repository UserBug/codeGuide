## Styles - Colors should be specified without opacity

Transparency makes the color dependent on the background.  
Therefore, their various combinations can lead to stylistic bugs.

##### ❌ BAD

```scss
$DARK_COLOR: rgba(#000000, .6);
```

```javascript
const DARK_COLOR = 'rgba(0, 0, 0, 0.8)';
```

##### ✔ GOOD

```scss
$DARK_COLOR: #222222;
```

```javascript
const DARK_COLOR = 'rgba(50, 50, 50)';
```

---

[Back to Code Guide - Styles](https://github.com/UserBug/codeGuide/tree/v2/docs/styles)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 