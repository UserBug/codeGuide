### Split Code - Slice Long Functions

Long functions most often indicate the presence of a sequence of
[Imperative programming](https://en.wikipedia.org/wiki/Imperative_programming) in them,  
it can be difficult to understand the long chain of sequential instructions.
It is recommended to separate sequential instructions into logical blocks  
and bring them into separate functions.  
You can choose the number that best suits your project, but the number must be hard-defined.

Clean Code by [Robert C. Martin](https://en.wikipedia.org/wiki/Robert_C._Martin):
_In the eighties we used to say that a function should be no bigger than a screen-full.  
Of course we said that at a time when VT100 screens were 24 lines by 80 columns,  
and our editors used 4 lines for administrative purposes.  
Nowadays with a cranked-down font and a nice big monitor,  
you can fit 150 characters on a line and a 100 lines or more on a screen.  
Lines should not be 150 characters long.  
Functions should not be 100 lines long.  
Functions should hardly ever be 20 lines long._

`max-lines-per-function: ["error", { "max": 50, "skipBlankLines": true, "skipComments": true }]`  
[eslint - max-lines-per-function](https://eslint.org/docs/latest/rules/max-lines-per-function)

##### ❌ BAD

```javascript
const updateCalendar = (timestamp) => {
    const date = new Date(timestamp);

    document.getElementById('day').innerHTML = date.getDate();
    document.getElementById('month').innerHTML = date.getMonth();
    document.getElementById('year').innerHTML = date.getFullYear();
    /* ... more repitable operations ... */
    document.getElementById('second').innerHTML = date.getSeconds();
    document.getElementById('minute').innerHTML = date.getMinutes();
    document.getElementById('hour').innerHTML = date.getHours();
    // more than 50 lines
};
```

##### ✔ GOOD

```javascript
// A small function containing a set of sequential commands combined logically
const updateDateAtCalendar = (date) => {
    document.getElementById('day').innerHTML = date.getDate();
    document.getElementById('month').innerHTML = date.getMonth();
    document.getElementById('year').innerHTML = date.getFullYear();
};

// A small function containing a set of sequential commands combined logically
const updateTimeAtCalendar = (date) => {
    document.getElementById('second').innerHTML = date.getSeconds();
    document.getElementById('minute').innerHTML = date.getMinutes();
    document.getElementById('hour').innerHTML = date.getHours();
};

const updateCalendar = (timestamp) => {
    const date = new Date(timestamp);

    // Larger blocks of lines are moved to separate functions, reducing the original
    updateDateAtCalendar(date);
    updateTimeAtCalendar(date);
};
```