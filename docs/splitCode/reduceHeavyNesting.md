### Split Code - Reduce Heavy nesting

Operators that increase the nesting of logic:  
`if for while switch`  
Each new level makes it harder to understand the code,  
forcing you to remember the context of all the nesting boxes.
In addition, it becomes much more difficult to track the scope of `let` and `const`.  
It is recommended to move the logic into separate new functions and methods.

[W3.org - Avoid heavy nesting](https://www.w3.org/wiki/JavaScript_best_practices#Avoid_heavy_nesting)

`max-depth: ["error", 2]`  
[eslint - max-depth](https://eslint.org/docs/latest/rules/max-depth)

##### ❌ BAD

```javascript
const moveSecondsСlockHand = (seconds) => {
    if (document.secondsСlockHand) {
        // Nested 1 deep
        if (typeof seconds === 'number') {
            // Nested 2 deep
            if (seconds <= 0) {
                // Nested 3 deep
                if (seconds >= 60) {
                    // Nested 4 deep
                    const minutes = Math.trunc(seconds / 60);
                    const otherSeconds = seconds = minutes * 60;
                    moveHoursСlockHand(minutes);
                    document.secondsСlockHand.move(otherSeconds);
                } else {
                    document.secondsСlockHand.move(seconds);
                }
            } else {
                throw new Error('Argument must be a positive number');
            }
        } else {
            throw new Error('Argument is not a number');
        }
    } else {
        throw new Error('secondsСlockHand is not set');
    }
};
```

##### ✔ GOOD

```javascript
const validateMoveSecondsСlockHandArguments = (seconds) => {
    if (typeof seconds === 'number') {
        // Nested 1 deep
        throw new Error('Argument is not a number');
    } else if (seconds <= 0) {
        // Nested 1 deep
        throw new Error('Argument must be a positive number');
    }
};

const validateIsSecondsСlockHandSet = () => {
    if (!this.secondsСlockHand) {
        // Nested 1 deep
        throw new Error('secondsСlockHand is not set');
    }
};

const moveSecondsСlockHand = (seconds) => {
    validateIsSecondsСlockHandSet();
    validateMoveSecondsСlockHandArguments(seconds);

    let moveOnSeconds = seconds;
    if (seconds >= 60) {
        // Nested 1 deep
        const minutes = Math.trunc(seconds / 60);
        const otherSeconds = seconds = minutes * 60;
        moveHoursСlockHand(minutes);
    }

    if (moveOnSeconds) {
        // Nested 1 deep
        document.secondsСlockHand.move(moveOnSeconds);
    }
};
```

[Back to Code Guide - Split Code](https://github.com/UserBug/codeGuide/tree/v2/docs/splitCode/index.md)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 