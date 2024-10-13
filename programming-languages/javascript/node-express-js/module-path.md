```jsx
const path = require('path')

// return basename of the file
console.log(path.basename(__filename));

//return dirname of the file
console.log(path.dirname(__filename));

//return file extension
console.log(path.extname(__filename));

//create path object
console.log(path.parse(__filename));

//concatenate path
console.log(path.join(__dirname, 'test', 'hello.html'));
```