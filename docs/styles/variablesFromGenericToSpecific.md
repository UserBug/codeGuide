## Styles - Variables from Generic to Specific

Using 3 levels of abstraction for style variables allows you to:

* Remove the number of duplicate styles
* Standardize the design system
* Clearly describe the purpose of each variable
* Easy to find collected in one place
* It becomes possible to see all values at once
* Easier to understand the system in styles
* Easy to change values for design author
* It's hard for a developer to hide their nonstandard styles.
* Inconsistencies or a wide variety of meanings are immediately visible.

#### Level 1 - Values

For encapsulating absolute values only.

* Stores only values
* Variables should NOT be used directly in component styles

__Name pattern__: `Adjective` `What it is ?`

```
MAIN_FONT
XL_INDENT
BOLD_FONT
RED_COLOR
```

#### Level 2 - Purpose

It is intended to describe the purpose.

* Get values only from "Level 1 - Values"
* Variables can be used directly in component styles

__Name pattern__: `Where will be used?` `Adjective` `What it is ?`

```
ROW_MAIN_FONT
BLOCK_HORIZONTAL_INDENT
LINK_BOLD_FONT
ERROR_TEXT_COLOR
```

#### Level 3 - Component

Describes UI component styles.

* Get values only from "Level 2 - Purpose"
* Variables can be used directly in component styles

__Name pattern__: `Component` `Where will be used?` `Adjective` `What it is ?`

```
MENU_ROW_MAIN_FONT
ARTICLE_BLOCK_HORIZONTAL_INDENT
LINK_BOLD_FONT
ERROR_POPUP_TEXT_COLOR
```

##### ❌ BAD

```css
:root {
    --RED: #c15454;
    --YELLOW:  #aeae00;
    --SIZE: 200px;
}

.button {
  color: var(--RED);
  background: var(--YELLOW);
  border: #333333;
  height: 20px;
  width: var(--SIZE);
}
```

```javascript
const root = {
    RED: "#c15454",
    YELLOW: "#aeae00",
    SIZE: "200px",
};

const button = {
  color: root.RED,
  background: root.YELLOW,
  border: "#333333",
  height: "20px",
  width: root.SIZE,
}
```

##### ✔ GOOD

```scss
// theme/colors.css
:root {
  // Level 1 - Values
  --MAIN_RED_COLOR: #c15454;
  --LIGHT_RED_COLOR: #e19494;
  --DARCK_RED_COLOR: #4e2222;
  --MAIN_YELLOW_COLOR: #aeae00;

  // Level 2 - Purpose
  --ERROR_COLOR: var(--MAIN_RED_COLOR);
  --ERROR_BORDER_COLOR: var(--LIGHT_RED_COLOR);
  --ERROR_BACKGROUND_COLOR: var(--LIGHT_RED_COLOR);
}
```

```scss
// theme/sizes.css
:root {
  --S_SIZE: 5px;
  --M_SIZE: 10px;
  --L_SIZE: 20px;
  --XL_SIZE: 40px;

  --ROW_HEIGHT: var(--L_SIZE);
  --ROW_VERTICAL_INDENT: var(--M_SIZE);
  --ROW_HORIZONTAL_INDENT: var(--S_SIZE);
  --BUTTON_HEIGHT: var(--L_SIZE);
}
```

```scss
// components/button.css
.button {
  height: var(--BUTTON_HEIGHT);
}
```

```scss
// components/submitButton.css
.submitButton {
  // Level 3 - Components
  --SUBMIT_BUTTON_HEIGHT: var(--BUTTON_HEIGHT);
  
  height: var(--SUBMIT_BUTTON_HEIGHT);
  line-height: var(--SUBMIT_BUTTON_HEIGHT);
}

.errorPopup {
  // Level 3 - Components
  --ERROR_POPUP_TEXT_COLOR: var(--ERROR_TEXT_COLOR);
  --ERROR_POPUP_BORDER_COLOR: var(--ERROR_FRAMING_COLOR);

  color: var(--ERROR_POPUP_TEXT_COLOR);
  border-color: var(--ERROR_POPUP_BORDER_COLOR);
}
```

```javascript
// theme/colors.js

const COLOR_VALUES = {
  // Level 1 - Values
  MAIN_RED_COLOR: "#c15454",
  LIGHT_RED_COLOR: "#e19494",
  DARCK_RED_COLOR: "#4e2222",
  MAIN_YELLOW_COLOR: "#aeae00",
};

const COLORS = {
  // Level 2 - Purpose
  ERROR_COLOR: COLOR_VALUES.MAIN_RED_COLOR,
  ERROR_BORDER_COLOR: COLOR_VALUES.LIGHT_RED_COLOR,
  ERROR_BACKGROUND_COLOR: COLOR_VALUES.LIGHT_RED_COLOR,
};
```

```javascript
// theme/sizes.js

const SIZE_VALUES = {
  // Level 1 - Values
  S_SIZE: 5,
  M_SIZE: 10,
  L_SIZE: 20, 
  XL_SIZE: 40,
};

const SIZE = {
  // Level 2 - Purpose
  ROW_HEIGHT: SIZE_VALUES.L_SIZE,
  ROW_VERTICAL_INDENT: SIZE_VALUES.M_SIZE,
  ROW_HORIZONTAL_INDENT: SIZE_VALUES.S_SIZE,
  BUTTON_HEIGHT: SIZE_VALUES.L_SIZE,
};
```

```javascript
// components/button.style.js
const BUTTON_STYLE = {
  // Level 3 - Components
  height: SIZE.BUTTON_HEIGHT,
};
```

```javascript
// components/submitButton.style.css
const SUBMIT_BUTTON_STYLE = {
  // Level 3 - Components
  height: SIZE.BUTTON_HEIGHT,
  lineHeight: SIZE.BUTTON_HEIGHT,
};

const ERROR_POPUP_STYLE = {
  // Level 3 - Components
  color: COLOR.ERROR_TEXT_COLOR,
  borderColor: COLOR.ERROR_FRAMING_COLOR,
}
```

---

[Back to Code Guide - Styles](https://github.com/UserBug/codeGuide/tree/v2/docs/styles)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 