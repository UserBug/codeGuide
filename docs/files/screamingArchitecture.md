## Screaming Architecture - Group files by modules and not by type

Much more often it is necessary to modify one particular module than all files with constants in the project. Therefore:

* It makes it easier to find all the files associated with the module.
* Repeatedly simplifies the replacement/modification of structure in the module.
* Each module becomes independent, and can be implemented using a different architecture that better meets the
  requirements.

[Screaming Architecture - Uncle Bob](https://blog.cleancoder.com/uncle-bob/2011/09/30/Screaming-Architecture.html)

##### ❌ BAD

```
root
    components
        grid
        button
        input
    constants
        grid
        button
        input
    reducers
        grid
        button
        input
```

##### ✔ GOOD

```
root
    grid
        component
        constants
        reducer
    button
        component
        constants
        reducer
    input
        component
        constants
        reducer
```

---

[Back to CodeGuide - Files](https://github.com/UserBug/codeGuide/tree/v2/docs/files)

[Back to CodeGuide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 