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

**11. Problem: Express Authentication Middleware**

**Problem Statement:**
Implement an authentication middleware for an Express application. The middleware should check for the presence of a valid JWT (JSON Web Token) in the request headers. If a valid token is present, allow the request to proceed; otherwise, return a 401 Unauthorized status.

**Function Signature:**
```javascript
/**
 * Authentication middleware for Express
 * @param {Object} req - Express request object
 * @param {Object} res - Express response object
 * @param {Function} next - Express next function
 */
function authenticationMiddleware(req, res, next) {
  // Your implementation here
}
```

**Expected Output:**
- If a valid JWT is present, allow the request to proceed.
- If no JWT is present or it's invalid, return a 401 Unauthorized status.

**Test Cases:**
1. Request with a valid JWT should proceed.
2. Request without a JWT or with an invalid JWT should return a 401 Unauthorized status.

**Solution:**
```javascript
const jwt = require('jsonwebtoken');

function authenticationMiddleware(req, res, next) {
  const token = req.headers.authorization;

  if (token) {
    try {
      const decoded = jwt.verify(token, 'secretKey');
      req.user = decoded;
      next();
    } catch (error) {
      res.status(401).json({ error: 'Invalid token' });
    }
  } else {
    res.status(401).json({ error: 'Token not provided' });
  }
}
```

---

**12. Problem: Express Rate Limiting**

**Problem Statement:**
Implement a rate-limiting middleware for an Express application. The middleware should limit the number of requests from a single IP address to a specified rate, and return a 429 Too Many Requests status if the limit is exceeded.

**Function Signature:**
```javascript
/**
 * Rate-limiting middleware for Express
 * @param {Object} req - Express request object
 * @param {Object} res - Express response object
 * @param {Function} next - Express next function
 */
function rateLimitMiddleware(req, res, next) {
  // Your implementation here
}
```

**Expected Output:**
- If the number of requests from a single IP is below the limit, allow the request to proceed.
- If the limit is exceeded, return a 429 Too Many Requests status.

**Test Cases:**
1. Send requests within the limit; all should proceed.
2. Send requests exceeding the limit; some should return a 429 status.

**Solution:**
```javascript
const rateLimit = require('express-rate-limit');

const limiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 100, // limit each IP to 100 requests per window
});

app.use(limiter);
```

---

**13. Problem: Express WebSocket Integration**

**Problem Statement:**
Extend an existing Express application to include WebSocket support. Create a WebSocket server that echoes back any message it receives from a client. Implement an endpoint "/websocket" that serves an HTML page with JavaScript to establish a WebSocket connection.

**Function Signature:**
```javascript
/**
 * WebSocket server for Express
 * @param {Object} server - HTTP server instance
 */
function setupWebSocket(server) {
  // Your implementation here
}
```

**Expected Output:**
- Clients should be able to establish a WebSocket connection to "/websocket".
- Messages sent by clients should be echoed back by the server.

**Test Cases:**
1. Establish a WebSocket connection and send a message; it should be echoed back.

**Solution:**
```javascript
const http = require('http');
const express = require('express');
const WebSocket = require('ws');

const app = express();
const server = http.createServer(app);

setupWebSocket(server);

app.get('/websocket', (req, res) => {
  // Serve HTML with JavaScript for WebSocket connection
  res.sendFile(__dirname + '/websocket.html');
});

server.listen(3000, () => {
  console.log('Server is running on port 3000');
});

function setupWebSocket(server) {
  const wss = new WebSocket.Server({ server });

  wss.on('connection', (ws) => {
    ws.on('message', (message) => {
      // Echo back the received message
      ws.send(message);
    });
  });
}
```

---

**14. Problem: Express Caching Middleware**

**Problem Statement:**
Implement a caching middleware for an Express application. The middleware should cache responses based on the request URL and return cached responses for subsequent identical requests. Allow cache expiration after a specified time.

**Function Signature:**
```javascript
/**
 * Caching middleware for Express
 * @param {Object} req - Express request object
 * @param {Object} res - Express response object
 * @param {Function} next - Express next function
 */
function cachingMiddleware(req, res, next) {
  // Your implementation here
}
```

**Expected Output:**
- Cached responses should be returned for identical requests within the cache expiration time.
- Subsequent requests after cache expiration should trigger a new response.

**Test Cases:**
1. Make a request, cache the response, and make the same request again within the cache expiration time.
2. Make a request, cache the response, wait for cache expiration, and make the same request again.

**Solution:**
```javascript
const NodeCache = require('node-cache');
const cache = new NodeCache({ stdTTL: 60 }); // Cache with a 60-second expiration

function cachingMiddleware(req, res, next) {
  const key = req.url;

  // Check if response is cached
  const cachedResponse = cache.get(key);

  if (cachedResponse) {
    res.send(cachedResponse);
  } else {
    // If not cached, proceed with the request
    res.sendResponse = res.send;
    res.send = (body) => {
      // Cache the response
      cache.set(key, body);
      res.sendResponse(body);
    };

    next();
  }
}
```

---

**15. Problem: Express Logging Middleware**

**Problem Statement:**
Create a logging middleware for an Express application. The middleware should log detailed information about each incoming request, including the timestamp, HTTP method, URL, request headers, and request body.

**Function Signature:**
```javascript
/**
 * Logging middleware for Express
 * @param {Object} req - Express request object
 * @param {Object} res - Express response object
 * @param {Function} next - Express next function
 */
function loggingMiddleware(req, res, next) {
  // Your implementation here
}
```

**Expected Output:**
- Each incoming request should be logged with detailed information.

**Test Cases:**
1. Make multiple requests and check the server logs for detailed information.

**Solution:**
```javascript
function loggingMiddleware(req, res, next) {
  const timestamp = new Date().toISOString();
  const method = req.method;
  const url = req.url;
  const headers = req.headers;
  const body = req.body;

  console.log(`
    Timestamp: ${timestamp}
    Method: ${method}
    URL: ${url}
    Headers: ${JSON.stringify(headers)}
    Body: ${JSON.stringify(body)}
  `);

  next();
}
```


**16. Problem: MongoDB Connection Setup**

**Problem Statement:**
Create an Express application with MongoDB integration using Mongoose. Implement a function to establish a connection to a MongoDB database. Ensure that the connection is successful and log a success message.

**Function Signature:**
```javascript
/**
 * Establishes a connection to MongoDB using Mongoose
 */
function connectToMongoDB() {
  // Your implementation here
}
```

**Expected Output:**
- If the connection is successful, log a success message.

**Test Cases:**
1. Call `connectToMongoDB()` and check the server logs for a successful connection message.

**Solution:**
```javascript
const mongoose = require('mongoose');

function connectToMongoDB() {
  mongoose.connect('mongodb://localhost/mydatabase', { useNewUrlParser: true, useUnifiedTopology: true });

  const db = mongoose.connection;

  db.on('error', console.error.bind(console, 'MongoDB connection error:'));
  db.once('open', () => {
    console.log('Connected to MongoDB successfully!');
  });
}

// Call the function to establish the connection
connectToMongoDB();
```

---

**17. Problem: Mongoose Schema and Model**

**Problem Statement:**
Define a Mongoose schema for a "User" with properties: "username" (string) and "email" (string). Create a Mongoose model for the User schema. Implement a function to add a new user to the MongoDB database.

**Function Signature:**
```javascript
/**
 * Adds a new user to the MongoDB database
 * @param {Object} user - User object with properties username and email
 */
function addUserToDatabase(user) {
  // Your implementation here
}
```

**Expected Output:**
- If the user is successfully added, log a success message.

**Test Cases:**
1. Call `addUserToDatabase({ username: 'john_doe', email: 'john@example.com' })` and check the server logs for a success message.

**Solution:**
```javascript
const mongoose = require('mongoose');

// Define User schema
const userSchema = new mongoose.Schema({
  username: String,
  email: String,
});

// Create User model
const User = mongoose.model('User', userSchema);

function addUserToDatabase(user) {
  const newUser = new User(user);

  newUser.save((err, savedUser) => {
    if (err) {
      console.error('Error adding user:', err);
    } else {
      console.log('User added successfully:', savedUser);
    }
  });
}

// Call the function to add a user
addUserToDatabase({ username: 'john_doe', email: 'john@example.com' });
```

---

**18. Problem: Express Route with MongoDB Query**

**Problem Statement:**
Create an Express route that retrieves all users from the MongoDB database and returns them as a JSON response.

**Function Signature:**
```javascript
/**
 * Express route to get all users from MongoDB
 * @param {Object} req - Express request object
 * @param {Object} res - Express response object
 */
function getAllUsers(req, res) {
  // Your implementation here
}
```

**Expected Output:**
- Return a JSON response with an array of user objects.

**Test Cases:**
1. Access the route `/users` and check if the response contains the expected user data.

**Solution:**
```javascript
const express = require('express');
const app = express();
const mongoose = require('mongoose');

// Define User schema and create User model (as shown in the previous solution)

// Express route to get all users
app.get('/users', getAllUsers);

function getAllUsers(req, res) {
  User.find({}, (err, users) => {
    if (err) {
      console.error('Error fetching users:', err);
      res.status(500).send('Internal Server Error');
    } else {
      res.json(users);
    }
  });
}

// Connect to MongoDB (as shown in the first solution)

// Start the Express server
app.listen(3000, () => {
  console.log('Server is running on port 3000');
});
```

---

**19. Problem: Mongoose Validation**

**Problem Statement:**
Enhance the user schema from the previous question to include validation for the "email" property (must be a valid email address). Implement a function to add a new user to the MongoDB database with validation.

**Function Signature:**
```javascript
/**
 * Adds a new user to the MongoDB database with validation
 * @param {Object} user - User object with properties username and email
 */
function addUserWithValidation(user) {
  // Your implementation here
}
```

**Expected Output:**
- If the user is successfully added, log a success message. If validation fails, log an error message.

**Test Cases:**
1. Call `addUserWithValidation({ username: 'john_doe', email: 'invalid-email' })` and check the server logs for a validation error message.

**Solution:**
```javascript
const userSchemaWithValidation = new mongoose.Schema({
  username: String,
  email: {
    type: String,
    required: true,
    unique: true,
    validate: {
      validator: function (value) {
        // Simple email validation
        const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        return emailRegex.test(value);
      },
      message: 'Invalid email format',
    },
  },
});

const UserWithValidation = mongoose.model('UserWithValidation', userSchemaWithValidation);

function addUserWithValidation(user) {
  const newUser = new UserWithValidation(user);

  newUser.save((err, savedUser) => {
    if (err) {
      console.error('Error adding user with validation:', err.message);
    } else {
      console.log('User added successfully with validation:', savedUser);
    }
  });
}

// Call the function to add a user with validation
addUserWithValidation({ username: 'john_doe', email: 'invalid-email' });
```

---

**20. Problem: Express Route with MongoDB Aggregation**

**Problem Statement:**
Create an Express route that uses MongoDB aggregation to calculate and return the average age of all users in the database.

**Function Signature:**
```javascript
/**
 * Express route to calculate the average age of all users in MongoDB
 * @param {Object} req - Express request object
 * @param {Object} res - Express response object
 */
function averageAgeOfUsers(req, res) {
  // Your implementation here
}
```

**Expected Output:**
- Return a JSON response with the calculated average age.

**Test Cases:**
1. Access the route `/average-age` and check if the response contains the expected average age.

**Solution:**
```javascript
// Assuming the userSchema includes an "age" property

function averageAgeOfUsers(req, res) {
  User.aggregate([
    {
      $group: {
        _id: null,
        averageAge: { $avg: '$age' },
      },
    },
  ], (err, result) => {
    if (err) {
      console.error('Error calculating average age:', err);
      res.status(500).send('Internal Server Error');
    } else {
      const averageAge = result[0] ? result[0].averageAge : 0;
      res.json({ averageAge });
    }
