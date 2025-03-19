# Nodejs
This repo consists of nodejs docs

# 📌 CommonJS vs. ES Modules in Node.js

Node.js supports **two module systems**:  
- **CommonJS (CJS)** – the traditional module system (`require`)  
- **ES Modules (ESM)** – the modern standard (`import`)  

## 🔹 Key Differences

| Feature             | CommonJS (CJS)                        | ES Modules (ESM)                    |
|---------------------|--------------------------------------|--------------------------------------|
| **File Extension**  | `.js` (default) / `.cjs`             | `.mjs` (or `.js` with `"type": "module"`) |
| **Import Syntax**   | `const fs = require('fs');`          | `import fs from 'fs';`              |
| **Export Syntax**   | `module.exports = {...}` / `exports.foo = bar;` | `export default foo;` / `export const bar = ...;` |
| **Asynchronous Support** | Synchronous by default       | Supports `import()` for dynamic imports |
| **JSON Imports**    | `require('./data.json')` (default)   | `import data from './data.json' assert { type: 'json' };` (Node.js 16+) |
| **__dirname & __filename** | Available by default       | Not available (use `import.meta.url`) |
| **Dynamic Imports** | Not supported natively             | Supported via `import()`            |
| **Browser Compatibility** | Not supported in browsers   | Works in browsers (with `<script type="module">`) |

## 🔹 Example Usage

### **CommonJS (CJS)**
```js
// utils.js
module.exports = {
  greet: (name) => `Hello, ${name}!`
};

// index.js
const utils = require('./utils');
console.log(utils.greet('World'));
```
### **ES module (mjs)**
```js
// utils.mjs
export const greet = (name) => `Hello, ${name}!`;

// index.mjs
import { greet } from './utils.mjs';
console.log(greet('World'));
```
