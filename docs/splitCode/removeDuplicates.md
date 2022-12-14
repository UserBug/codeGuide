### Split Code - Remove Duplicates
The presence of duplicates in the code indicates  
that the same operation has been performed several times in the most non-optimal way.
Although copying working pieces of code can greatly speed up the development of concepts and projects,  
it makes maintenance much more difficult later on. 
* Changes in a repetitive operation have to be made in many files, it is easy to make a mistake. 
* It is often difficult to find a specific error location among dozens of copies of an operation.

It is recommended to immediately move repeating blocks into separate functions.  
And strive to reduce the metric indicating the number of duplicates.

[SonarQube - Metric - Duplications](https://docs.sonarqube.org/latest/user-guide/metric-definitions/#duplications)

##### ❌ BAD

```javascript
const compareTwoPages = async ({pageOneId, pageTwoId}) => {

    const fileOnePromise = fsPromises.readFile(
        `pagesDir/${pageOneId}.html`,
        {encoding: 'utf8'}
    );

    const fileTwoPromise = fsPromises.readFile(
        `pagesDir/${pageTwoId}.html`,
        {encoding: 'utf8'}
    );

    return (await fileOnePromise) === (await fileTwoPromise);
};
```

##### ✔ GOOD

```javascript
const readPageFile = (pageId) => (
    fsPromises.readFile(
        `pagesDir/${pageOneId}.html`,
        {encoding: 'utf8'}
    )
);

const compareTwoPages = async ({pageOneId, pageTwoId}) => {

    const fileOnePromise = readPageFile(pageOneId);
    const fileTwoPromise = readPageFile(pageTwoId);

    return (await fileOnePromise) === (await fileTwoPromise);
};
```