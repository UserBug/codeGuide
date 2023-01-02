## React - Always memorize components

To prevent unnecessary rerender of component and increases performance,  
each component should be memorized.  
Use recommended ways:

* shouldComponentUpdate
* extends React.PureComponent (Be careful, PureComponent correctly checks only immutable properties, objects are checked
  by reference.)
* React.memo

[reactjs.org - shouldComponentUpdate In Action](https://reactjs.org/docs/optimizing-performance.html#shouldcomponentupdate-in-action)

---

[Back to Code Guide - React](https://github.com/UserBug/codeGuide/tree/v2/docs/react)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 