### Split Code - Sustain Single Responsibility

Single Responsibility is one of key programing principals included to [SOLID](https://en.wikipedia.org/wiki/SOLID)  
this approach helps get rid of one of the worst and most common [God object](https://en.wikipedia.org/wiki/God_object)
patterns.  
By creating and dedicating one simple and clear task to each function, you simultaneously:

* Make it easier to understand
* Make it reusable in the future
* Facilitate refactoring and collaboration

Signs that a function violates the single responsibility principle:

* Contains a direct call to more than 1 third party library or API
* Contains instructions for performing more than 2 operations
* You find it hard to come up with a name quickly or the name contains abstract words

You will definitely not be able to achieve a perfect separation of concerns  
due to development time constraints and the frequency of business requirement changes.  
However, if 80% of your functions are pure, this is the ideal result,  
which will greatly facilitate and speed up development.

[Single-responsibility principle](https://en.wikipedia.org/wiki/Single-responsibility_principle)  
[W3.org - Modularize - one function per task](https://www.w3.org/wiki/JavaScript_best_practices#Modularize_.E2.80.94_one_function_per_task)

##### ❌ BAD

```javascript
const getPage = async ({pageId}) => {
    console.log('Start read'); // Logging operation

    const pageContent = (
        await fsPromises.readFile( // Direc usage of third party API
            `pagesDir/${pageId}.html`, // Create path operation
            {encoding: 'utf8'} // Store configuration for third party
        )
    );

    console.log('End read'); // Logging operation

    return pageContent;
};
```

##### ✔ GOOD

```javascript
// logger.js - Contain logic only about "How to log"
const writeLog = ({message, data}) => (
    console.log(message, data)
);
```

```javascript
// fileService.js - Contain logic only about "How to work with files"
const createFilePath = ({ directory, fileName }) => (
  `${directory}/${fileName}`
);

const DEFAULT_FILE_PARAMS = { encoding: 'utf8' };

const readFile = (filePath) => (
  fsPromises.readFile(
    filePath,
    DEFAULT_FILE_PARAMS
  )
);
```

```javascript
// pageService.js - Contain logic only about "How to work with Pages"
const PAGES_DIRECTORY = 'pageDir';
const PAGES_FILE_FORMAT = 'html';

const createPageFilePath = (pageId) => (
  createFilePath({
    directory: PAGES_DIRECTORY,
    fileName: `${pageId}.${PAGES_FILE_FORMAT}`
  })
);

const readPageContent = (pageId) => (
  readFile(
    createPageFilePath(pageId)
  )
);
```

```javascript
// resolver.js - Contain buisness workflow sequence, 
// without implementation details of each step
const getPage = async ({ pageId }) => {
  writeLog('Start read');
  const pageContent = readPageContent(pageId);
  writeLog('End read');
  return pageContent;
};
```