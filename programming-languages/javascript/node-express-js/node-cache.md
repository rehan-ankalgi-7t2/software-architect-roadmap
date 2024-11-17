# Node Cache

```bash
npm install node-cache
```

```jsx
const express = require('express');
const NodeCache = require('node-cache');

const app = express();
const port = 3000;

// Initialize an in-memory cache
const cache = new NodeCache();

// Middleware function for API caching
const cacheMiddleware = (req, res, next) => {
  const key = req.originalUrl || req.url;

  // Check if the data is in the cache
  const cachedData = cache.get(key);

  if (cachedData) {
    // If data is found in the cache, send the cached response
    console.log('Cache hit for:', key);
    return res.json(cachedData);
  }

  // If data is not in the cache, continue with the request
  next();
};

// Example API endpoint with caching
app.get('/api/data', cacheMiddleware, (req, res) => {
  // Simulate fetching data from a database or another API
  const data = {
    message: 'This is the data from the API',
    timestamp: new Date().toISOString(),
  };

  // Cache the data for 60 seconds (adjust as needed)
  cache.set(req.originalUrl || req.url, data, 60);

  // Send the response to the client
  res.json(data);
});

// Start the server
app.listen(port, () => {
  console.log(`Server is running on http://localhost:${port}`);
});
```

In this example:

- The **`node-cache`** library is used to create an in-memory cache.
- The **`cacheMiddleware`** function checks if the requested data is in the cache. If it is, the cached response is sent to the client, and the request is short-circuited.
- If the data is not in the cache, the request continues, and the actual API endpoint (**`/api/data`**) returns the data.
- The fetched data is then stored in the cache with a specified expiration time (60 seconds in this case).

Note: This is a basic example using in-memory caching. In a production environment, you might want to consider more advanced caching strategies, such as using a distributed caching system or integrating with a caching proxy like Redis.

Keep in mind that caching strategies should be chosen based on the specific requirements and characteristics of your application.