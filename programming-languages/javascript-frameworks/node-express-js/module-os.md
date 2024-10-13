```jsx
const os = require('os');

//platform
console.log(os.platform());

//CPU architecture
console.log(os.arch());

//CPU core info
console.log(os.cpus());

//amount of free memory & total memory
console.log(os.freemem(), os.totalmem());

//home directory
console.log(os.homedir());

//uptime
console.log(os.uptime(), os.userInfo());
```