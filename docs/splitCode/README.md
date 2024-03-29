## Split Code

This document was created to define clear criteria and ways to refactor code.  
Although the principles described are universal in themselves,  
the absolute meanings described in them may be adapted  
depending on the context of the project and development.

Also remember that due to development time constraints and constantly changing business requirements,  
you will not be able to achieve a perfect result.  
But keeping 80% of your code clean is more than great and will allow you to save in a project:

* [Maintainability](https://en.wikipedia.org/wiki/Maintainability)
* [Scalability](https://en.wikipedia.org/wiki/Scalability)
* [Extensibility](https://en.wikipedia.org/wiki/Extensibility)
* [Observability](https://en.wikipedia.org/wiki/Observability)

### Cognitive Complexity

An objective metric for identifying refactoring sites can be "Cognitive Complexity".
Its high scores clearly indicate files that need improvement.
All approaches described here are aimed at reducing the overall complexity in each file.  
[CodeClimate - Cognitive Complexity](https://docs.codeclimate.com/docs/cognitive-complexity)  
[G. Ann Campbell - SonarSource - Cognitive Complexity](https://www.sonarsource.com/docs/CognitiveComplexity.pdf)  
[eslint-plugin-sonarjs - cognitive-complexity](https://github.com/SonarSource/eslint-plugin-sonarjs/blob/master/docs/rules/cognitive-complexity.md)  
[JetBrains - plugin - CognitiveComplexity](https://plugins.jetbrains.com/plugin/12024-cognitivecomplexity)

---

### Move Out Nested callbacks

[Move Out Nested callbacks - read more](https://github.com/UserBug/codeGuide/tree/v2/docs/splitCode/moveOutNestedCallbacks.md)  
It is recommended to allow only 1 level of nesting.
Deeper nesting can be fixed by
[Dependency injection](https://en.wikipedia.org/wiki/Dependency_injection) through
[Higher-order function](https://en.wikipedia.org/wiki/Higher-order_function#JavaScript).

---

### Reduce Heavy nesting

[Reduce Heavy nesting - read more](https://github.com/UserBug/codeGuide/tree/v2/docs/splitCode/reduceHeavyNesting.md)  
It is recommended to allow only 2 level of nesting,  
move the logic into separate new functions and methods.

---

### Remove Duplicates

[Remove Duplicates - read more](https://github.com/UserBug/codeGuide/tree/v2/docs/splitCode/removeDuplicates.md)  
It is recommended to immediately move duplicated blocks into separate functions.  
And strive to reduce the metric indicating the number of duplicates.

---

### Shorten Files

[Shorten Files - read more](https://github.com/UserBug/codeGuide/tree/v2/docs/splitCode/shortenFiles.md)  
The number of lines of code can serve as a trigger for the need to split a file.  
It is recommended to shorten files to a maximum length of 250 lines.  
To do this, you can turn larger files into folders,  
moving all independent functions into new small files.

---

### Slice Long Functions

[Slice Long Functions - read more](https://github.com/UserBug/codeGuide/tree/v2/docs/splitCode/sliceLongFunctions.md)  
It can be difficult to understand the long chain of sequential instructions.
It is recommended to separate sequential instructions into logical blocks  
and bring them into separate functions.

---

### Use One "third party API" per file

[Use One "third party API" per file - read more](https://github.com/UserBug/codeGuide/tree/v2/docs/splitCode/useOneThirdPartyApiPerFile.md)  
Transferring the direct use of third-party libraries and APIs into separate modules (Adapters)  
helps to isolate the business logic from the implementation details of the tools.

---

### Sustain Single Responsibility

[Sustain Single Responsibility - read more](https://github.com/UserBug/codeGuide/tree/v2/docs/splitCode/sustainSingleResponsibility.md)  
By creating and dedicating one simple and clear task to each function, you simultaneously:

* Make it easier to understand
* Make it reusable in the future
* Facilitate refactoring and collaboration

---

##### ❌ BAD

```javascript
const compareTwoPages = async ({pageOneId, pageTwoId}) => {
    console.log(`Start read pages: ${pageOneId}; ${pageTwoId}`);

    const fileOnePromise = fsPromises.readFile(
        `pagesDir/${pageOneId}.html`,
        {encoding: 'utf8'}
    ).then((fileContent) => {
        console.log(`File read: pagesDir/${pageOneId}.html`);
        return fileContent;
    }).catch((error) => {
        console.error(`Cant read file: pagesDir/${pageOneId}.html`, error)
        throw new Error(`Cant read page: ${pageOneId}`);
    });

    const fileTwoPromise = fsPromises.readFile(
        `pagesDir/${pageTwoId}.html`,
        {encoding: 'utf8'}
    ).then((fileContent) => {
        console.log(`File read: pagesDir/${pageTwoId}.html`);
        return fileContent;
    }).catch((error) => {
        console.error(`Cant read file: pagesDir/${pageTwoId}.html`, error)
        throw new Error(`Cant read page: ${pageTwoId}`);
    });

    return (await fileOnePromise) === (await fileTwoPromise);
};

```

##### ✔ GOOD

```javascript
// logger
const writeLog = ({message, data}) => (
    console.log(message, data)
);

const writeError = ({message, error}) => (
    console.log(message, error)
);
```

```javascript
// array helpers
const isAllInArrayAreEqual = (arr) => (
    arr.every((element) => element === arr[0])
);
```

```javascript
// file service
const DEFAULT_FILE_PARAMS = {encoding: 'utf8'};

const createFilePath = ({directory, fileName}) => (
    `${directory}/${fileName}`
);

const readFileContent = async (filePath) => (
    await fsPromises.readFile(
        filePath,
        DEFAULT_FILE_PARAMS
    )
);
````

```javascript
// pages service
const PAGES_DIRECTORY = 'pageDir';
const PAGES_FILE_FORMAT = 'html';

const createPageFilePath = (pageId) => (
    createFilePath({
        directory: PAGES_DIRECTORY,
        fileName: `${pageId}.${PAGES_FILE_FORMAT}`
    })
);
```

```javascript
// compareTwoPages resolver
const handlePageReadError = ({filePath, error}) => {
    writeError({message: `Cant read file: pagesDir/${filePath}.html`, error})
    throw new Error(`Cant read page: ${filePath}`);
};

const readPageContent = (pageId) => {
    const filePath = createPageFilePath(pageId);

    writeLog(`File read: ${filePath}`);

    return readFileContent(filePath).catch((error) => {
        handlePageReadError({filePath, error});
    });
};

const compareTwoPages = async ({pageOneId, pageTwoId}) => {
    const pagesArray = [pageOneId, pageTwoId];

    writeLog({message: `Start read pages: ${pagesArray.join('; ')}`});

    return await isAllInArrayAreEqual(
        await Promise.all(
            pagesArray.map(readPageContent)
        )
    );
}
```
  
[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 
