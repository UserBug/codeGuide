## React - Do not use context

One of the most important reason:  
Parents did not know about context that need for children.  
This can lead to a lack of updates in children.  
Main idea of React is Components, they are "lazy" and react only on Props change.  
(PS: That's why library called "React")

If you want change something in child Component you should set new Props to it.

* All Props are as clear and visible as possible.  
  But the context remains hidden and unseen.  
  This leads to a misunderstanding of code and data source on the page,  
  which greatly increases the number of bugs and the time to resolve them.
* Props have strict typing and involved in the life cycle of the component.
* Passing data through props give possibility to use clear ways of memorization.

Context does not have these advantages.

Official React documentation say:  
"If you only want to avoid passing some props through many levels, component composition is often a simpler solution
than context."  
[reactjs.org - Before You Use Context](https://reactjs.org/docs/context.html#before-you-use-context)

> After the release of React 16.3, the context became much safer.
> Despite this, the context should be used only in
> special exceptional cases.

---

[Back to Code Guide - React](https://github.com/UserBug/codeGuide/tree/v2/docs/react)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 