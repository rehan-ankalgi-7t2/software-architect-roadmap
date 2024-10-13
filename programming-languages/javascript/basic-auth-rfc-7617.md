# Basic Auth (RFC 7617)

<aside style="padding: 16px; background-color: #555">
💡 Given the name “Basic Authentication”, you should not confuse Basic Authentication with the standard username and password authentication. Basic authentication is a part of the HTTP specification, and the details can be <a href="https://www.rfc-editor.org/rfc/rfc7617.html">found in the RFC7617</a>.

</aside>

Because it is a part of the HTTP specifications, all the browsers have native support for “HTTP Basic Authentication”.

<img src="https://mdn.github.io/shared-assets/images/diagrams/http/authentication/basic-auth.svg" style="background-color: white;">

## Implementation in node js

npm dependency:

```jsx
npm i base64-js
```

> auth.middleware.js
> 

```jsx
const base64 = require('base-64');

function decodeCredentials(authHeader) {
  const encodedCredentials = authHeader.trim().replace(/Basic\s+/i, '');
	
	const decodedCredentials = base64.decode(encodedCredentials);

	return decodedCredentials.split(':');
}

module.exports = function protect(req, res, next) {
  // Take the header and decode credentials
  const [username, password] = decodeCredentials(
    req.headers.authorization || ''
  );

  // Verify the credentials
  if (username === 'admin' && password === 'admin') {
    return next();
  }

  // Respond with authenticate header on auth failure.
  res.set('WWW-Authenticate', 'Basic realm="user_pages"');
  res.status(401).send('Authentication required.');
};
```