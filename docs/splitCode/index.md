## Split Code

This document was created to define clear criteria and ways to refactor code.
Although the principles described are universal in themselves, the absolute meanings described in them may be adapted
depending on the context of the project and development.

---

### Move Out Nested callbacks

[Move Out Nested callbacks - example](./moveOutNestedCallbacks.md)  
It is recommended to allow only 1 level of nesting.
Deeper nesting can be fixed by
[Dependency injection](https://en.wikipedia.org/wiki/Dependency_injection) through
[Higher-order function](https://en.wikipedia.org/wiki/Higher-order_function#JavaScript).

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

