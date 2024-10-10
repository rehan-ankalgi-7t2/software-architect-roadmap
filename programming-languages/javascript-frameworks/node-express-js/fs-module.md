Node.js provides a built-in module called `fs` (File System) for performing file operations. The `fs` module allows you to interact with the file system in a way modeled on standard POSIX functions.

### Basic File Operations

### 1. Reading Files

You can read files asynchronously or synchronously using the `fs` module.

**Asynchronous Reading:**

```jsx
const fs = require('fs');

// Asynchronously read a file
fs.readFile('example.txt', 'utf8', (err, data) => {
  if (err) {
    console.error('Error reading file:', err);
    return;
  }
  console.log('File content:', data);
});

```

**Synchronous Reading:**

```jsx
const fs = require('fs');

// Synchronously read a file
try {
  const data = fs.readFileSync('example.txt', 'utf8');
  console.log('File content:', data);
} catch (err) {
  console.error('Error reading file:', err);
}

```

### 2. Writing Files

You can write data to a file asynchronously or synchronously.

**Asynchronous Writing:**

```jsx
const fs = require('fs');

// Asynchronously write to a file
fs.writeFile('example.txt', 'Hello, World!', 'utf8', (err) => {
  if (err) {
    console.error('Error writing to file:', err);
    return;
  }
  console.log('File has been written');
});

```

**Synchronous Writing:**

```jsx
const fs = require('fs');

// Synchronously write to a file
try {
  fs.writeFileSync('example.txt', 'Hello, World!', 'utf8');
  console.log('File has been written');
} catch (err) {
  console.error('Error writing to file:', err);
}

```

### 3. Appending to Files

You can append data to a file asynchronously or synchronously.

**Asynchronous Appending:**

```jsx
const fs = require('fs');

// Asynchronously append to a file
fs.appendFile('example.txt', '\\nAppended content', 'utf8', (err) => {
  if (err) {
    console.error('Error appending to file:', err);
    return;
  }
  console.log('Content has been appended');
});

```

**Synchronous Appending:**

```jsx
const fs = require('fs');

// Synchronously append to a file
try {
  fs.appendFileSync('example.txt', '\\nAppended content', 'utf8');
  console.log('Content has been appended');
} catch (err) {
  console.error('Error appending to file:', err);
}

```

### 4. Deleting Files

You can delete files asynchronously or synchronously.

**Asynchronous Deletion:**

```jsx
const fs = require('fs');

// Asynchronously delete a file
fs.unlink('example.txt', (err) => {
  if (err) {
    console.error('Error deleting file:', err);
    return;
  }
  console.log('File has been deleted');
});

```

**Synchronous Deletion:**

```jsx
const fs = require('fs');

// Synchronously delete a file
try {
  fs.unlinkSync('example.txt');
  console.log('File has been deleted');
} catch (err) {
  console.error('Error deleting file:', err);
}

```

### Advanced File Operations

### 5. Reading and Writing File Metadata

You can use `fs.stat` and `fs.statSync` to read file metadata.

**Asynchronous Reading Metadata:**

```jsx
const fs = require('fs');

// Asynchronously read file metadata
fs.stat('example.txt', (err, stats) => {
  if (err) {
    console.error('Error reading file stats:', err);
    return;
  }
  console.log('File stats:', stats);
});

```

**Synchronous Reading Metadata:**

```jsx
const fs = require('fs');

// Synchronously read file metadata
try {
  const stats = fs.statSync('example.txt');
  console.log('File stats:', stats);
} catch (err) {
  console.error('Error reading file stats:', err);
}

```

### 6. Creating Directories

You can create directories asynchronously or synchronously using `fs.mkdir` and `fs.mkdirSync`.

**Asynchronous Directory Creation:**

```jsx
const fs = require('fs');

// Asynchronously create a directory
fs.mkdir('exampleDir', { recursive: true }, (err) => {
  if (err) {
    console.error('Error creating directory:', err);
    return;
  }
  console.log('Directory created');
});

```

**Synchronous Directory Creation:**

```jsx
const fs = require('fs');

// Synchronously create a directory
try {
  fs.mkdirSync('exampleDir', { recursive: true });
  console.log('Directory created');
} catch (err) {
  console.error('Error creating directory:', err);
}

```

### 7. Watching Files for Changes

You can watch files for changes using `fs.watch`.

**Watching Files:**

```jsx
const fs = require('fs');

// Watch for changes in a file
fs.watch('example.txt', (eventType, filename) => {
  if (filename) {
    console.log(`File ${filename} has been modified. Event type: ${eventType}`);
  }
});

```

### Summary

- **Reading Files**: `fs.readFile` (asynchronous), `fs.readFileSync` (synchronous)
- **Writing Files**: `fs.writeFile` (asynchronous), `fs.writeFileSync` (synchronous)
- **Appending to Files**: `fs.appendFile` (asynchronous), `fs.appendFileSync` (synchronous)
- **Deleting Files**: `fs.unlink` (asynchronous), `fs.unlinkSync` (synchronous)
- **Reading File Metadata**: `fs.stat` (asynchronous), `fs.statSync` (synchronous)
- **Creating Directories**: `fs.mkdir` (asynchronous), `fs.mkdirSync` (synchronous)
- **Watching Files**: `fs.watch`

By leveraging the `fs` module, you can perform a wide range of file operations efficiently in your Node.js applications.