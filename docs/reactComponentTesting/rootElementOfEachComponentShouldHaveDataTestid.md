## React Component testing - Root element of each component should have "data-testid"

"component-***"  
This practice will allow you not only to make functional testing more convenient,  
but also to easily distinguish component blocks in html.

```javascript
const myBlock = () => (
  <div data-testid="component-myBlock">Block</div>
);
```

---

[Back to Code Guide - React Component testing](https://github.com/UserBug/codeGuide/tree/v2/docs/reactComponentTesting)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 