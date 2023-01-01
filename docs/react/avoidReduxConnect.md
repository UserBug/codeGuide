## React - Avoid Redux “connect”

When some component "connect()" to Redux it create new wrapper,  
this is another component in the tree and another code to execute before rendering.  
All "mapStateToProps" of all components in the application will be called for any action in the application. This often
leads to unnecessary rendering.  
Try to use "connect()" only for Compounds like "Page" which are controlled by router and only one of the routes will be
displayed.  
Next, pass the data through the flow of "Props".

---

[Back to Code Guide - React](https://github.com/UserBug/codeGuide/tree/v2/docs/react)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 