## JavaScript - Use arrow functions

in all cases when you don't need context of this particular function.

[npm - eslint-plugin-prefer-arrow-functions](https://www.npmjs.com/package/eslint-plugin-prefer-arrow-functions)  
[Google - JS Styleguide - Features functions arrow functions](https://google.github.io/styleguide/jsguide.html#features-functions-arrow-functions)
[When should I use Arrow functions in ECMAScript 6?](https://stackoverflow.com/questions/22939130/when-should-i-use-arrow-functions-in-ecmascript-6)

##### ❌ BAD

```javascript
function sum({a, b}) {
    return a + b;
}
```

##### ✔ GOOD

```javascript
const sum = ({a, b}) => (a + b); // "sum" is named arrow function which has name in stacktrace
```

[Back to CodeGuide - JavaScript](https://github.com/UserBug/codeGuide/tree/v2/docs/javaScript)

[Back to CodeGuide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 