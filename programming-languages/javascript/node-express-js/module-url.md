```jsx
const url = require('url');

const myurl = new URL('http://mywebsite.com/hello.html?id=100&status=active');

//serialized url
console.log(myurl.href);

//host (root domain)
console.log(myurl.host);

//pathname
console.log(myurl.pathname);

//serialized query
console.log(myurl.search);

//params object
console.log(myurl.searchParams);

//appending params dynamically
myurl.searchParams.append('abc', '123');
console.log(myurl.searchParams);

//looping through the params
myurl.searchParams.forEach((value, name) => console.log(`${name} : ${value}`));
```