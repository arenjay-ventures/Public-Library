---
layout: default
title: Node.js Cheatsheet
parent: Tools & Technology
grand_parent: References
nav_order: 7
---

# Node.js Cheatsheet

## **What is Node.js?**

Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine that allows you to run JavaScript on the server side. It's essential for:
- **Backend Development**: APIs, web servers, microservices
- **Full-Stack JavaScript**: Use same language for frontend and backend
- **Real-time Applications**: WebSockets, chat apps, gaming
- **DevOps**: Build tools, automation scripts
- **Career Growth**: High demand for Node.js developers

## **Installation & Setup**

### **Install Node.js**
```bash
# Download from nodejs.org or use package manager
# Windows: Download installer from nodejs.org
# macOS: brew install node
# Linux: sudo apt install nodejs npm

# Verify installation
node --version
npm --version
```

### **Node Version Manager (NVM)**
```bash
# Install NVM (Linux/macOS)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash

# Use NVM
nvm install node        # Install latest Node.js
nvm install 18.17.0     # Install specific version
nvm use 18.17.0         # Switch to version
nvm list               # List installed versions
```

## **Core Concepts**

### **Event Loop**
Node.js uses an event-driven, non-blocking I/O model:
```javascript
// Non-blocking example
console.log('Start');
setTimeout(() => console.log('Timeout'), 0);
console.log('End');
// Output: Start, End, Timeout
```

### **Modules System**
```javascript
// CommonJS (Node.js default)
const fs = require('fs');
const path = require('path');

// ES6 Modules (with "type": "module" in package.json)
import fs from 'fs';
import path from 'path';
```

## **Essential APIs**

### **File System (fs)**
```javascript
const fs = require('fs');
const path = require('path');

// Synchronous operations
const data = fs.readFileSync('file.txt', 'utf8');
fs.writeFileSync('output.txt', 'Hello World');

// Asynchronous operations
fs.readFile('file.txt', 'utf8', (err, data) => {
    if (err) throw err;
    console.log(data);
});

// Promises (Node.js 14+)
const fsPromises = require('fs').promises;
async function readFile() {
    try {
        const data = await fsPromises.readFile('file.txt', 'utf8');
        console.log(data);
    } catch (err) {
        console.error(err);
    }
}
```

### **HTTP Module**
```javascript
const http = require('http');

// Create server
const server = http.createServer((req, res) => {
    res.writeHead(200, { 'Content-Type': 'text/plain' });
    res.end('Hello World');
});

server.listen(3000, () => {
    console.log('Server running on port 3000');
});
```

### **Path Module**
```javascript
const path = require('path');

// Common path operations
path.join('folder', 'file.txt');        // folder/file.txt
path.resolve('folder', 'file.txt');     // /absolute/path/folder/file.txt
path.dirname('/folder/file.txt');       // /folder
path.basename('/folder/file.txt');      // file.txt
path.extname('file.txt');               // .txt
```

### **URL Module**
```javascript
const url = require('url');

const myUrl = new URL('https://example.com:8080/path?name=value#hash');
console.log(myUrl.hostname);    // example.com
console.log(myUrl.port);        // 8080
console.log(myUrl.pathname);    // /path
console.log(myUrl.search);      // ?name=value
```

## **Package Management**

### **npm Commands**
```bash
# Initialize project
npm init
npm init -y              # Skip questions

# Install packages
npm install package      # Install and save to package.json
npm install -g package   # Install globally
npm install --save-dev package  # Install as dev dependency

# Package management
npm list                 # List installed packages
npm outdated            # Check for updates
npm update              # Update packages
npm uninstall package   # Remove package

# Scripts
npm run script-name     # Run script from package.json
npm start               # Run start script
npm test                # Run test script
```

### **package.json**
```json
{
  "name": "my-app",
  "version": "1.0.0",
  "description": "My Node.js application",
  "main": "index.js",
  "scripts": {
    "start": "node index.js",
    "dev": "nodemon index.js",
    "test": "jest"
  },
  "dependencies": {
    "express": "^4.18.0"
  },
  "devDependencies": {
    "nodemon": "^2.0.0"
  }
}
```

## **Popular Frameworks**

### **Express.js**
```javascript
const express = require('express');
const app = express();

// Middleware
app.use(express.json());
app.use(express.static('public'));

// Routes
app.get('/', (req, res) => {
    res.send('Hello World');
});

app.get('/api/users', (req, res) => {
    res.json({ users: [] });
});

app.post('/api/users', (req, res) => {
    const { name, email } = req.body;
    res.json({ message: 'User created', user: { name, email } });
});

app.listen(3000, () => {
    console.log('Server running on port 3000');
});
```

### **Express Middleware**
```javascript
// Custom middleware
app.use((req, res, next) => {
    console.log(`${req.method} ${req.path}`);
    next();
});

// Error handling middleware
app.use((err, req, res, next) => {
    console.error(err.stack);
    res.status(500).send('Something broke!');
});
```

## **Async Programming**

### **Callbacks**
```javascript
// Traditional callback
fs.readFile('file.txt', 'utf8', (err, data) => {
    if (err) {
        console.error(err);
        return;
    }
    console.log(data);
});
```

### **Promises**
```javascript
// Using promises
const fsPromises = require('fs').promises;

fsPromises.readFile('file.txt', 'utf8')
    .then(data => console.log(data))
    .catch(err => console.error(err));
```

### **Async/Await**
```javascript
// Modern async/await
async function readFile() {
    try {
        const data = await fsPromises.readFile('file.txt', 'utf8');
        console.log(data);
    } catch (err) {
        console.error(err);
    }
}
```

## **Environment Variables**

### **Using dotenv**
```bash
# Install dotenv
npm install dotenv
```

```javascript
// Load environment variables
require('dotenv').config();

// Access variables
const port = process.env.PORT || 3000;
const dbUrl = process.env.DATABASE_URL;
```

### **.env file**
```env
PORT=3000
DATABASE_URL=mongodb://localhost:27017/myapp
API_KEY=your-secret-key
NODE_ENV=development
```

## **Error Handling**

### **Try-Catch**
```javascript
async function riskyOperation() {
    try {
        const result = await someAsyncOperation();
        return result;
    } catch (error) {
        console.error('Error:', error.message);
        throw error; // Re-throw if needed
    }
}
```

### **Process Events**
```javascript
// Handle uncaught exceptions
process.on('uncaughtException', (err) => {
    console.error('Uncaught Exception:', err);
    process.exit(1);
});

// Handle unhandled promise rejections
process.on('unhandledRejection', (reason, promise) => {
    console.error('Unhandled Rejection at:', promise, 'reason:', reason);
    process.exit(1);
});
```

## **Testing**

### **Jest**
```bash
# Install Jest
npm install --save-dev jest
```

```javascript
// test.js
const { add, multiply } = require('./math');

test('adds 1 + 2 to equal 3', () => {
    expect(add(1, 2)).toBe(3);
});

test('multiplies 2 * 3 to equal 6', () => {
    expect(multiply(2, 3)).toBe(6);
});
```

### **Running Tests**
```bash
npm test                # Run tests
npm test -- --watch    # Watch mode
npm test -- --coverage # Coverage report
```

## **Database Integration**

### **MongoDB with Mongoose**
```javascript
const mongoose = require('mongoose');

// Connect to MongoDB
mongoose.connect('mongodb://localhost:27017/myapp');

// Define schema
const userSchema = new mongoose.Schema({
    name: String,
    email: String,
    age: Number
});

// Create model
const User = mongoose.model('User', userSchema);

// CRUD operations
async function createUser() {
    const user = new User({ name: 'John', email: 'john@example.com' });
    await user.save();
}

async function getUsers() {
    const users = await User.find();
    return users;
}
```

### **SQL with Sequelize**
```javascript
const { Sequelize, DataTypes } = require('sequelize');

// Connect to database
const sequelize = new Sequelize('database', 'username', 'password', {
    host: 'localhost',
    dialect: 'mysql'
});

// Define model
const User = sequelize.define('User', {
    name: DataTypes.STRING,
    email: DataTypes.STRING
});

// CRUD operations
async function createUser() {
    const user = await User.create({ name: 'John', email: 'john@example.com' });
    return user;
}
```

## **Development Tools**

### **Nodemon**
```bash
# Install nodemon
npm install -g nodemon

# Use nodemon
nodemon app.js          # Auto-restart on file changes
```

### **Debugging**
```javascript
// Using debugger
debugger; // Set breakpoint

// Using console
console.log('Debug info:', variable);
console.error('Error:', error);
console.table(data);    // Display data as table
```

### **Performance Monitoring**
```javascript
// Using console.time
console.time('operation');
// ... some operation
console.timeEnd('operation');

// Memory usage
console.log(process.memoryUsage());
```

## **Deployment**

### **Environment Setup**
```javascript
// Check environment
if (process.env.NODE_ENV === 'production') {
    // Production settings
    app.use(express.static('build'));
} else {
    // Development settings
    app.use(express.static('public'));
}
```

### **PM2 Process Manager**
```bash
# Install PM2
npm install -g pm2

# Start application
pm2 start app.js

# Monitor
pm2 monit

# Restart
pm2 restart app

# Stop
pm2 stop app
```

## **Best Practices**

### **Code Organization**
```javascript
// Separate routes
// routes/users.js
const express = require('express');
const router = express.Router();

router.get('/', (req, res) => {
    res.json({ users: [] });
});

module.exports = router;

// app.js
const userRoutes = require('./routes/users');
app.use('/api/users', userRoutes);
```

### **Error Handling**
```javascript
// Global error handler
app.use((err, req, res, next) => {
    console.error(err.stack);
    res.status(500).json({ error: 'Something went wrong!' });
});
```

### **Security**
```javascript
// Use helmet for security headers
const helmet = require('helmet');
app.use(helmet());

// Rate limiting
const rateLimit = require('express-rate-limit');
const limiter = rateLimit({
    windowMs: 15 * 60 * 1000, // 15 minutes
    max: 100 // limit each IP to 100 requests per windowMs
});
app.use(limiter);
```

## **Learning Resources**

### **Documentation**
- **[Node.js Official Docs](https://nodejs.org/docs/)** - Official documentation
- **[Express.js Docs](https://expressjs.com/)** - Express framework guide
- **[npm Documentation](https://docs.npmjs.com/)** - Package manager docs

### **Tutorials**
- **[Node.js Tutorial](https://www.tutorialspoint.com/nodejs/)** - Comprehensive tutorial
- **[Express.js Guide](https://expressjs.com/en/guide/routing.html)** - Express routing guide
- **[MongoDB with Node.js](https://www.mongodb.com/developer/languages/javascript/node-crud-tutorial/)** - Database integration

### **Practice Projects**
- **REST API** with Express
- **Real-time Chat** with Socket.io
- **File Upload** system
- **Authentication** with JWT
- **Microservices** architecture

Remember: **Node.js is about asynchronous programming**. Master callbacks, promises, and async/await. Start with simple scripts, then build web applications, and finally work on complex systems. The JavaScript ecosystem is vast - focus on the fundamentals first!