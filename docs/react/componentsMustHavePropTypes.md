## React - Components must have PropTypes

This basic rule helps to identify and avoid many errors.  
PropTypes provide dynamic typing at the development stage.  
What neither TypeScript nor JSDoc can`t provide.

When using TypeScript, the component interfaces must be compiled to PropTypes for development bundle.  
[babel-plugin-typescript-to-proptypes](https://www.npmjs.com/package/babel-plugin-typescript-to-proptypes)

[reactjs.org - Typechecking With PropTypes](https://reactjs.org/docs/typechecking-with-proptypes.html)  
[eslint - react/prop-types](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/prop-types.md)

```javascript
SomeComponent.propTypes = {
  name: PropTypes.string.isRequired
};
```

In TypeScript, it is best to write properties in the form of interfaces, this will allow them to be reused:

##### ✔ GOOD

```typescript
interface BudgetProps {
    readonly budgeted: number,
    readonly spent: number,
    readonly category?: string,
}

interface DepartmentProps extends BudgetProps {
    readonly id: string;
}

const DepartmentOverview: React.FC<DepartmentProps> = (props: DepartmentProps) => {}
```

---

[Back to Code Guide - React](https://github.com/UserBug/codeGuide/tree/v2/docs/react)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov