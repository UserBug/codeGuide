## React Hooks

### Basics
As a first step please read article from Facebook:  
[reactjs - Hooks rules](https://reactjs.org/docs/hooks-rules.html)  

* Don’t call Hooks inside loops, conditions, or nested functions.
* Only Call Hooks from React Functions
* A custom Hook is a JavaScript function whose name starts with ”use” and that may call other Hooks.

---

### Naming of useState
To clearly identify the variables working with the state, we should use prefixes:  
```state***``` and ```setState***```  

##### ❌ BAD
```javascript
const [count, setCount] = useState(0);
```

##### ✔ GOOD 
```javascript
const [stateCount, setStateCount] = useState(0);
```

---

### Hooks as independent files
All Hooks should be implemented as independent functions and files.  
What benefits from it:

* The size of the component has been reduced, which increases its readability.
* Component logic is divided into clear blocks with human-readable names.
* All dependencies of each logic block are clearly distinguished,  
hidden closures become explicit arguments.
* With the increase in business logic, each hook can be independently scaled.
* Initially declares the hook as a block of logic that can be reused.
* Such an implementation is a declarative programming approach that  
helps to separate actions from their implementation practices.

---
Copyright © 2017 Stanislav Kochenkov 
