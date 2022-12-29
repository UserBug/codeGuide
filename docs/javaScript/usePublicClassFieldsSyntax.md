## JavaScript - Use public class fields syntax

Use the constructor only when necessary,  
otherwise define public properties and methods in the class body.

* Reduce amount of code
* Autobinding

[React doc - Handling events](https://reactjs.org/docs/handling-events.html)   
[React doc - Autobinding](https://reactjs.org/docs/react-without-es6.html#autobinding)

##### ❌ BAD

```javascript
class Basket {
    constructor() {
        this.count = 0;
        this.handleAdd = this.handleAdd.bind(this);
    }

    handleAdd({add}) {
        this.count += add;
    }
}
```

##### ✔ GOOD

```javascript
class Basket {
    count = 0;

    handleAdd = ({add}) => {
        this.count += add;
    };
}
```

[Back to CodeGuide - JavaScript](https://github.com/UserBug/codeGuide/tree/v2/docs/javaScript)

[Back to CodeGuide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 