### Problem 1: File Reader

**Problem Statement:**
Create a function `readFileContent(filePath)` that takes the path to a file as input and reads its content asynchronously using the `fs` module. The function should print the content to the console.

**Function Signature:**
```javascript
function readFileContent(filePath) {
    // Implementation
}
```

**Expected Output:**
```
File Content:
This is the content of the file.
Hello, Node.js!
```

**Test Cases:**
```javascript
readFileContent('test-files/file1.txt');
// Expected Output: Content of file1.txt

readFileContent('test-files/empty-file.txt');
// Expected Output: (empty string)

readFileContent('test-files/nonexistent-file.txt');
// Expected Output: Error reading file: ENOENT: no such file or directory...
```

**Solution:**
```javascript
const fs = require('fs');

function readFileContent(filePath) {
    fs.readFile(filePath, 'utf8', (err, data) => {
        if (err) {
            console.error(`Error reading file: ${err.message}`);
            return;
        }
        console.log(`File Content:\n${data}`);
    });
}

// Example usage
readFileContent('test-files/file1.txt');
```

### Problem 2: File Writer

**Problem Statement:**
Create a function `writeToFile(filePath, content)` that takes the path to a file and user input content as input. The function should write the content to the specified file using the `fs` module.

**Function Signature:**
```javascript
function writeToFile(filePath, content) {
    // Implementation
}
```

**Expected Output:**
```
Data written to output.txt
```

**Test Cases:**
```javascript
writeToFile('test-files/output1.txt', 'Sample content.');
// Expected Output: Data written to output1.txt

writeToFile('test-files/nonexistent-folder/output.txt', 'Content in a non-existent folder.');
// Expected Output: Error writing to file: ENOENT: no such file or directory...
```

**Solution:**
```javascript
const fs = require('fs');
const readline = require('readline');

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

function writeToFile(filePath, content) {
    fs.writeFile(filePath, content, 'utf8', (err) => {
        if (err) {
            console.error(`Error writing to file: ${err.message}`);
            return;
        }
        console.log(`Data written to ${filePath}`);
    });
}

// Example usage
rl.question('Enter content to write to file: ', (content) => {
    writeToFile('test-files/output.txt', content);
    rl.close();
});
```

### Problem 3: Execute Command

**Problem Statement:**
Create a function `executeCommand(command)` that takes a shell command as input and executes it using the `child_process` module. The function should print the output of the command to the console.

**Function Signature:**
```javascript
function executeCommand(command) {
    // Implementation
}
```

**Expected Output:**
```
Command Output:
File1.txt
File2.txt
```

**Test Cases:**
```javascript
executeCommand('ls -la');
// Expected Output: (output of ls -la)

executeCommand('echo "Hello, Node.js!"');
// Expected Output: Hello, Node.js!
```

**Solution:**
```javascript
const { exec } = require('child_process');

function executeCommand(command) {
    exec(command, (err, stdout, stderr) => {
        if (err) {
            console.error(`Error executing command: ${err.message}`);
            return;
        }
        console.log(`Command Output:\n${stdout}`);
    });
}

// Example usage
executeCommand('ls -la');
```

### Problem 4: Resolve Path

**Problem Statement:**
Create a function `resolvePath(relativePath)` that takes a relative path as input and resolves it to an absolute path using the `path` module. The function should print the resolved path to the console.

**Function Signature:**
```javascript
function resolvePath(relativePath) {
    // Implementation
}
```

**Expected Output:**
```
Resolved Path: /Users/username/project/folder/file.txt
```

**Test Cases:**
```javascript
resolvePath('../project/folder/file.txt');
// Expected Output: Resolved Path: /Users/username/project/folder/file.txt

resolvePath('nonexistent-folder/file.txt');
// Expected Output: Resolved Path: /Users/username/nonexistent-folder/file.txt
```

**Solution:**
```javascript
const path = require('path');

function resolvePath(relativePath) {
    const absolutePath = path.resolve(relativePath);
    console.log(`Resolved Path: ${absolutePath}`);
}

// Example usage
resolvePath('../project/folder/file.txt');
```

### Problem 5: File Extension Checker

**Problem Statement:**
Create a function `checkFileExtension(filePath, expectedExtension)` that takes a file path and an expected file extension as input. The function should check if the file has the expected extension using the `path` module and print the result to the console.

**Function Signature:**
```javascript
function checkFileExtension(filePath, expectedExtension) {
    // Implementation
}
```

**Expected Output:**
```
File has the expected extension: .txt
```

**Test Cases:**
```javascript
checkFileExtension('test-files/file1.txt', '.txt');
// Expected Output: File has the expected extension: .txt

checkFileExtension('test-files/image.png', '.jpg');
// Expected Output: File does not have the expected extension. Expected: .jpg, Actual: .png
```

**Solution:**
```javascript
const path = require('path');

function checkFileExtension(filePath, expectedExtension) {
    const actualExtension = path.extname(filePath).toLowerCase();
    if (actualExtension === expectedExtension) {
        console.log(`File has the expected extension: ${expectedExtension}`);
    } else {
        console.log(`File does not have the expected extension. Expected: ${expectedExtension}, Actual: ${actualExtension}`);
    }
}

// Example usage
checkFileExtension('test-files/file1.txt', '.txt');
```


**6. Problem: Express Route Handling**

**Problem Statement:**
You are building a web application using Express in Node.js. Create an Express route to handle GET requests to the endpoint "/greet" that takes a query parameter "name" and returns a personalized greeting. If the name parameter is not provided, the default greeting should be "Hello, Guest!".

**Function Signature:**
```javascript
/**
 * Handles GET requests to "/greet" endpoint
 * @param {Object} req - Express request object
 * @param {Object} res - Express response object
 */
function greetHandler(req, res) {
  // Your implementation here
}
```

**Expected Output:**
- If the "name" parameter is provided: "Hello, {name}!"
- If the "name" parameter is not provided: "Hello, Guest!"

**Test Cases:**
1. Request to `/greet?name=John` should return "Hello, John!"
2. Request to `/greet` should return "Hello, Guest!"

**Solution:**
```javascript
function greetHandler(req, res) {
  const name = req.query.name || 'Guest';
  res.send(`Hello, ${name}!`);
}
```

---

**7. Problem: Express Middleware**

**Problem Statement:**
Implement an Express middleware function that logs the timestamp and the HTTP method of every incoming request to the server.

**Function Signature:**
```javascript
/**
 * Express middleware to log incoming requests
 * @param {Object} req - Express request object
 * @param {Object} res - Express response object
 * @param {Function} next - Express next function
 */
function requestLoggerMiddleware(req, res, next) {
  // Your implementation here
}
```

**Expected Output:**
Log entries in the server console should be in the format: `{timestamp} - {HTTP method} request received`.

**Test Cases:**
1. Any incoming request should trigger the middleware and log the appropriate message.

**Solution:**
```javascript
function requestLoggerMiddleware(req, res, next) {
  console.log(`${new Date().toISOString()} - ${req.method} request received`);
  next();
}
```

---

**8. Problem: Express Error Handling**

**Problem Statement:**
Create an Express route that throws an error if the request parameter "number" is not a positive integer. Implement an error handling middleware to catch and handle this specific error, returning a custom error message and a 400 Bad Request status.

**Function Signature:**
```javascript
/**
 * Express route to handle requests with a positive integer parameter
 * @param {Object} req - Express request object
 * @param {Object} res - Express response object
 */
function positiveIntegerHandler(req, res) {
  // Your implementation here
}
```

**Expected Output:**
- If "number" is a positive integer: Return a success message.
- If "number" is not a positive integer: Trigger an error handled by the error handling middleware.

**Test Cases:**
1. Request to `/positive?number=5` should return a success message.
2. Request to `/positive?number=-2` should trigger the error handling middleware.

**Solution:**
```javascript
function positiveIntegerHandler(req, res) {
  const number = parseInt(req.query.number);

  if (Number.isInteger(number) && number > 0) {
    res.send('Success!');
  } else {
    throw new Error('Invalid positive integer');
  }
}

function errorHandler(err, req, res, next) {
  res.status(400).send(`Error: ${err.message}`);
}
```

---

**9. Problem: Express Static Files**

**Problem Statement:**
Create an Express application that serves static files (e.g., HTML, CSS, images) from a "public" directory. Ensure that accessing the root ("/") returns the "index.html" file from the "public" directory.

**Function Signature:**
```javascript
/**
 * Express application serving static files from the "public" directory
 * @param {Object} req - Express request object
 * @param {Object} res - Express response object
 */
function staticFileServer(req, res) {
  // Your implementation here
}
```

**Expected Output:**
Accessing the root ("/") should return the content of "public/index.html".

**Test Cases:**
1. Request to `/` should return the content of "public/index.html".
2. Request to `/styles/style.css` should return the content of "public/styles/style.css".

**Solution:**
```javascript
const express = require('express');
const path = require('path');

const app = express();

// Serve static files from the "public" directory
app.use(express.static(path.join(__dirname, 'public')));

// Define a route for the root ("/") to serve "public/index.html"
app.get('/', staticFileServer);

// Start the Express server
app.listen(3000, () => {
  console.log('Server is running on port 3000');
});
```

---

**10. Problem: Express Body Parsing**

**Problem Statement:**
Implement an Express route that handles POST requests to the "/add" endpoint. The route should expect a JSON object with two properties: "num1" and "num2". Return the sum of these two numbers.

**Function Signature:**
```javascript
/**
 * Handles POST requests to "/add" endpoint
 * @param {Object} req - Express request object
 * @param {Object} res - Express response object
 */
function addNumbersHandler(req, res) {
  // Your implementation here
}
```

**Expected Output:**
The response should be a JSON object with the sum of "num1" and "num2".

**Test Cases:**
1. POST request to `/add` with JSON body `{"num1": 3, "num2": 7}` should return `{"result": 10}`.
2. POST request to `/add` with invalid JSON body should return an error.

**Solution:**
```javascript
const express = require('express');

const app = express();

// Middleware to parse JSON in the request body
app.use(express.json());

// Route to handle POST requests to "/add"
app.post('/add', addNumbersHandler);

function addNumbersHandler(req, res) {
  const { num1, num2 } = req.body;

  if (typeof num1 === 'number' && typeof num2 === 'number') {
    const result = num1 + num2;
    res.json({ result });
  } else {
    res.status(400).json({ error: 'Invalid input' });
  }
}

// Start the Express server
app.listen(3000, () => {
  console.log('Server is running on port 3000');
});
```