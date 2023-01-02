## JavaScript - Prefer single return

It will be a single place you have to look to trace backwards and figure out what a function returns.  
Easier to debug and easier to modify.  
Multiple returns create interrupts in function execution,  
making it harder to find unused code.

[airbnb - single return vs multiple returns](https://github.com/airbnb/javascript/issues/761)  
[Anthony Steele - Single Return Law](https://www.anthonysteele.co.uk/TheSingleReturnLaw.html)

##### Opposite opinion

[Szymon Krajewski - Why should you return early?](https://szymonkrajewski.pl/why-should-you-return-early/)  
[Early exit - most common deviation from structured programming](https://en.wikipedia.org/wiki/Structured_programming#Early_exit)

##### ❌ BAD

```javascript
const sayMyName = (who) => {
    if (who === 'David Guetta') {
        return `${who}: Say my name, say my name\n If you love me, let me hear you.`;
    } else if (who === 'Breaking Bad') {
        return `${who}: You all know exactly who I am. Say my name.`
    }
    return `${who}: I do not know.`;
};
```

##### ✔ GOOD

```javascript
const sayMyName = (who) => {
    let partOfText = `${who}: I do not know.`;
    if (who === 'David Guetta') {
        partOfText = `${who}: Say my name, say my name\n If you love me, let me hear you.`;
    } else if (who === 'Breaking Bad') {
        partOfText = `${who}: You all know exactly who I am. Say my name.`
    }
    return partOfText;
};
```

---

[Back to Code Guide - JavaScript](https://github.com/UserBug/codeGuide/tree/v2/docs/javaScript)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 