## React Component testing - Do not test Snapshots

Comparing the two parts of the markup can only reveal that they are not the same.  
In most cases, the user doesn't care about the markup. is it ```<div>``` or ```<span>```.  
First of all, tests should check the correctness of behavior and logic of interaction with components.  
Tests based on Snapshots will fail if a minor change is made,  
although the behavior of the component remains correct.

---

[Back to Code Guide - React Component testing](https://github.com/UserBug/codeGuide/tree/v2/docs/reactComponentTesting)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 