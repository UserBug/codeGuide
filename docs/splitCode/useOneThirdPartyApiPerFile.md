### Split Code - Use One "third party API" per file
This rule is a strong simplification of one of the principles of Hexagonal architecture.  
Transferring the direct use of third-party libraries and APIs into separate modules (Adapters)  
helps to isolate the business logic from the implementation details of the tools.  
This allows you to do most of the changes and even the replacement of the tool independently  
and without touching the business logic.  

[Wiki - Hexagonal architecture](https://en.wikipedia.org/wiki/Hexagonal_architecture_(software))  
[Hexagonal architecture by example](https://blog.allegro.tech/2020/05/hexagonal-architecture-by-example.html)

##### ❌ BAD

```javascript
const getPage = async ({ pageId }) => {
  console.log('Start read'); // Call of logging API
  
  const pageContent = (
    await fsPromises.readFile( // Call of files API
      `pagesDir/${pageId}.html`,
      { encoding: 'utf8' }
    )
  );

  console.log('End read'); // Call of logging API
  
  return pageContent;
};
```

##### ✔ GOOD

```javascript
// logger.js - Adapter for Logging
const writeLog = ({ message, data }) => (
  console.log(message, data)
);
```

```javascript
// fileService.js - Adapter for Files operations
const readPageFile = (pageId) => (
  fsPromises.readFile(
    `pagesDir/${pageOneId}.html`,
    { encoding: 'utf8' }
  )
);
```

```javascript
// resolver.js
const getPage = async ({ pageId }) => {
  writeLog('Start read');

  const pageContent = await readPageFile(pageId);

  writeLog('End read');

  return pageContent;
};
```
