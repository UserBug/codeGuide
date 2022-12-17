### Split Code - Slice Long Functions
Long functions most often indicate the presence of a sequence of 
[Imperative programming](https://en.wikipedia.org/wiki/Imperative_programming) in them,  
it can be difficult to understand the long chain of sequential instructions.
It is recommended to separate sequential instructions into logical blocks  
and bring them into separate functions.  

`max-nested-callbacks: ["error", { "max": 50, "skipBlankLines": true, "skipComments": true }]`  
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