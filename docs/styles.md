## Styles

### Dont use inline styles
Inline styles have a big impact on application performance:

* To display them, the browser has to transform the string into a style for each item in each render
* Styles are duplicated many times for many elements in DOM
* The DOM tree increases many times in size

"using the style attribute as the primary means of styling elements is generally not recommended"    
[reactjs - style](https://reactjs.org/docs/dom-elements.html#style)  
[reactjs - Are inline styles bad?](https://reactjs.org/docs/faq-styling.html#are-inline-styles-bad)

##### ❌ BAD
```javascript
render() {
    return (
      <div style={{ color: myColorVar }}/>
    );
}
```

##### ✔ GOOD 
```scss
.container {
  color: $MY_COLOR_VAR;
}
```
```javascript
import style from './myComponent.scss';

render() {
    return (
      <div className={style.container}/>
    );
}
```

---

### Prefer class agents long child selectors
Long tag selectors tie styles to the structure of components.  
The hierarchy of elements within a component can change frequently,  
which immediately breaks styles.  
To prevent this, create and use more class names.  

##### ❌ BAD
```scss
.myComponent > div > div {}
```

##### ✔ GOOD 
```scss
.myComponent .header {}
```

---

### Avoid useless nesting
##### ❌ BAD
```scss
.myComponent {
    & > .focused {

    }
}
```

##### ✔ GOOD 
```scss
myComponent .focused {

}
```

---
### Use global class .RTL and .LTR to made different style for language direction
Style of Components should be separated from they structure.  
It helps to do less changes in JSX and reuse components.  
Complicated styles for different languages can be solved only by SCSS  

##### ❌ BAD
```scss
.rtl {
    transform: rotate(90deg);
    transform-origin: center;
}

.rtl {
    transform: rotate(-90deg);
    transform-origin: center;
}
```
```javascript
render() {
    return (
      <Icon className={isRTL ? style.rtl : style.ltr} />
    );
}

```

##### ✔ GOOD 
```scss
.icon {
  transform-origin: center;
}

:global(.RTL) .icon {
  transform: rotate(90deg);
}

:global(.LTR) .icon {
  transform: rotate(-90deg);
}
```
```javascript
render() {
    return (
      <Icon className={style.icon} />
    );
}
```

---

### SCSS Variables and Naming conventions
Use variables for all numerical values, quantities, and sizes excluding atomic (0, 100%, etc.)  
All variables should be placed in the general theme files and distributed according to their purpose (sizes, indents, colors, borders, shadows etc.).  
This will improve the visibility of the project and allow you to quickly change them.  

---

### Use css variables
If the requirements of your project allow you to use pure css constants - do it.  
This will allow you to:  

* Store style constants in one place
* Change styles dynamically with css

[mozilla - CSS variables Browser compatibility](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties#Browser_compatibility)

```scss
// theme/colors.scss
:root {
  --PRIMARY_DARK_COLOR: #213943;
  --PRIMARY_LIGHT_COLOR: #78909c;
  --PRIMARY_VERY_LIGHT_COLOR: #a7c0cd;
}

$PRIMARY_DARK_COLOR: var(--PRIMARY_DARK_COLOR);
$PRIMARY_LIGHT_COLOR: var(--PRIMARY_LIGHT_COLOR);
$PRIMARY_VERY_LIGHT_COLOR: var(--PRIMARY_VERY_LIGHT_COLOR);
```

---

### Variables from Generic to Specific
Using 2 levels of abstraction for style variables allows you to:

* Remove the number of duplicate styles
* Standardize the design system
* Clearly describe the purpose of each variable

##### ❌ BAD
```scss
$RED: #c15454;
$YELLOW: #aeae00;
$TOP_BLOCK_HEIGHT: 20px;
$LINE_WIDTH: 12px;

.header {
  color: $RED;
  background: $YELLOW;
  border: $RED;
  height: $TOP_BLOCK_HEIGHT;
  width: $LINE_WIDTH;

  .row {
    width: $LINE_WIDTH;
  }
}
```

##### ✔ GOOD 
```scss
// theme/colors.scss
:root {
  --RED: #c15454;
  --YELLOW:  #aeae00;

  --ERROR_COLOR: var(--RED);
  --ERROR_BORDER_COLOR: var(--RED);
  --ERROR_BACKGROUND_COLOR: var(--YELLOW);
}

$ERROR_COLOR: var(--ERROR_COLOR);
$ERROR_BORDER_COLOR: var(--ERROR_BORDER_COLOR);
$ERROR_BACKGROUND_COLOR: var(--ERROR_BACKGROUND_COLOR);
```
```scss
// theme/size.scss
:root {
  --SMAL_BLOCK_HEIGHT: 20px;
  --COLUMN_WIDTH: 12px;

  --ERROR_BLOCK_HEIGHT: var(--SMAL_BLOCK_HEIGHT);
  --ERROR_BLOCK_WIDTH: var(--COLUMN_WIDTH);
}

$ERROR_BLOCK_HEIGHT: var(--ERROR_BLOCK_HEIGHT);
$ERROR_BLOCK_WIDTH: var(--ERROR_BLOCK_WIDTH);
```

```scss
@import 'theme/colors';
@import 'theme/size';

.header {
  color: $ERROR_COLOR;
  background: $ERROR_BACKGROUND_COLOR;
  border: $ERROR_BORDER_COLOR;
  height: $ERROR_BLOCK_HEIGHT;
  width: $ERROR_BLOCK_WIDTH;

  .row {
    width: $ERROR_BLOCK_WIDTH;
  }
}
```

---

### Colors should be specified without opacity
Transparency makes the color dependent on the background.  
Therefore, their various combinations can lead to stylistic bugs.  

##### ❌ BAD
```scss
$DARK_COLOR: rgba(#000000, .6);
```

##### ✔ GOOD 
```scss
$DARK_COLOR: #222222;
```

---
Copyright © 2017 Stanislav Kochenkov 
