## Styles - Use global class .RTL and .LTR
to made different style for language direction.
Style of Components should be separated from they structure.  
It helps to do less changes in JSX and reuse components.  
Complicated styles for different languages can be solved only by SCSS

##### ❌ BAD

```scss
.rtl {
    transform: rotate(90deg);
    transform-origin: center;
}

.rtl {
    transform: rotate(-90deg);
    transform-origin: center;
}
```

```javascript
render() {
    return (
      <Icon className={isRTL ? style.rtl : style.ltr} />
    );
}

```

##### ✔ GOOD

```scss
.icon {
  transform-origin: center;
}

:global(.RTL) .icon {
  transform: rotate(90deg);
}

:global(.LTR) .icon {
  transform: rotate(-90deg);
}
```

```javascript
render() {
    return (
      <Icon className={style.icon} />
    );
}
```

---

[Back to Code Guide - Styles](https://github.com/UserBug/codeGuide/tree/v2/docs/styles)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 