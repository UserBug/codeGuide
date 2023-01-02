## Styles - Do not use inline styles

Inline styles have a big impact on application performance:

* To display them, the browser has to transform the string into a style for each item in each render
* Styles are duplicated many times for many elements in DOM
* The DOM tree increases many times in size

"using the style attribute as the primary means of styling elements is generally not recommended"    
[reactjs - style](https://reactjs.org/docs/dom-elements.html#style)  
[reactjs - Are inline styles bad?](https://reactjs.org/docs/faq-styling.html#are-inline-styles-bad)

##### ❌ BAD

```javascript
render() {
    return (
      <div style={{ color: myColorVar }}/>
    );
}
```

##### ✔ GOOD

```scss
.container {
  color: $MY_COLOR_VAR;
}
```

```javascript
import style from './myComponent.scss';

render() {
    return (
      <div className={style.container}/>
    );
}
```

---

[Back to Code Guide - Styles](https://github.com/UserBug/codeGuide/tree/v2/docs/styles)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 