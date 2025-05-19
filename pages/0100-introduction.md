<!-- # Getting Ready for Next.js -->
# Getting Ready for Next.js

Essential Web Fundamentals You Should Know Before diving into Next.js, you should be familiar with:

- **🧾 HTML**: Basic structure, elements, attributes, and forms
- **🎨 CSS**: Selectors, properties, layouts (Flexbox/Grid), responsive design
- **⚙️ JavaScript**: ES6+ features, including:
  - Arrow functions
  - Template literals
  - Destructuring
  - Spread/rest operators
  <!-- - Promises and async/await -->
  - Array methods (map, filter, reduce)

[//]: # "- **Git**: Basic version control concepts"
[//]: # "- **Command Line**: Basic terminal/command prompt usage"

- **📦 NPM**: Package management concepts

<!--
ก่อนที่จะไปทำความรู้จักกับ NextJS 
 NPM/YARN เครื่องมือที่ช่วยให้เราติดตั้งและจัดการเครื่องมืออื่นๆ ที่จำเป็นต่อการสร้างเว็บด้วย Next.js ได้ง่ายและรวดเร็ว
 เปรียบง่ายๆ ===>เหมือน "App Store" สำหรับนักพัฒนา

ถ้าเราจะสร้างเว็บ เราต้องติดตั้งเครื่องมือ/ตัวช่วย เช่น Next.js → ให้ช่วยโหลดมาให้
-->

---

# Modern Web App Essentials

Key Concepts You’ll Use Modern web applications like React & Next.js

- **User Interface (UI)**: What users see and interact with
- **Routing**: Navigation between different pages
- **Data Fetching**: Loading data from external sources
- **Rendering**: Converting code to user interface
- **State Management**: Managing application data
- **Authentication**: User identity verification
- **Security**: Protecting against vulnerabilities

---
level: 1
---

# Single Page Applications (SPAs) - React, Vue, ...

## ⚡What is a SPA?

A Single Page Application (SPA) is a web application that loads a single HTML page and dynamically updates the content as the user interacts with the app, without reloading the entire page.

---
layout: two-cols-header
level: 2
---

# Traditional Websites vs. SPAs

::left::

**Traditional Websites:**

- Each user action (clicking a link) triggers a request to the server
- Server returns a completely new HTML page
- Browser reloads the entire page (white flash, reset scroll position)
- Slower user experience, especially on slower connections

::right::

**Single Page Applications:**

- Initial page load gets the HTML, CSS, and JavaScript
- Subsequent interactions update only parts of the page
- No complete page reloads
- Feels more like a desktop application

[//]: # "::bottom::"
[//]: #
[//]: # "Next.js supports both SPAs and traditional multi-page applications."

---
hide: true
level: 2
---

# How SPAs Work

1. **Initial Load**: Browser loads the HTML, CSS, and JavaScript bundles
2. **JavaScript Takes Control**: JS code initializes and renders the application
3. **User Interactions**: When users click links or buttons:
   - JavaScript intercepts these actions
   - Updates the URL without refreshing the page
   - Fetches needed data (usually JSON) from APIs
   - Updates only the parts of the page that need to change

---
hide: false
---

## Benefits for Users

- **Smoother Experience**: No jarring page reloads
- **Faster Interactions**: Only new data is transferred, not entire pages
- **Responsive UI**: Interface remains interactive while data loads
- **Offline Capabilities**: Can work without constant internet connection

## Examples

Popular SPAs you might use every day:

- 📧 Gmail - Emails update without page reloads
- 👥 Facebook - Timeline updates dynamically
- 🔁 Twitter - New tweets appear without refreshing
- 🧭 Google Maps - Map updates as you navigate

Next.js supports both SPAs and traditional multi-page applications, giving you the best of both worlds.

<!-- insert more images Ex. App -->

---

# Essential JavaScript for React

Next.js is built on React, which requires these JavaScript concepts:

#### Functions and Arrow Functions

```javascript
// Regular function
function add(a, b) {
  return a + b;
}

// Arrow function
const add = (a, b) => a + b;
```
<!-- Function คือ "ชุดคำสั่ง" ที่เอาไว้ทำงานบางอย่าง เช่น คำนวณเลข, หรือจัดการข้อมูล
เหมือน สูตรสำเร็จ ที่เราเขียนไว้ แล้วเรียกใช้เมื่อไหร่ก็ได้ -->
---
hideInToc: true
class: py-6
---

#### Objects and Arrays

```javascript
// Objects
const user = {
  name: "John",
  age: 30,
  isAdmin: true,
};

// Arrays
const numbers = [1, 2, 3, 4, 5];
```

#### Array Methods

```javascript
const numbers = [1, 2, 3, 4, 5];

// map: transform each element
const doubled = numbers.map((num) => num * 2);
// [2, 4, 6, 8, 10]

// filter: keep elements that pass a test
const evenNumbers = numbers.filter((num) => num % 2 === 0);
// [2, 4]

// reduce: accumulate values
const sum = numbers.reduce((total, num) => total + num, 0);
// 15
```
<!-- Object คือ กล่องที่เก็บข้อมูลหลายอย่าง ในรูปแบบ (key - value)
ในที่นี้เหมือนแฟ้มข้อมูลของคนหนึ่งคน 
.filter(): คัดเฉพาะตัวที่ "ผ่านเงื่อนไข"
.reduce(): “รวมค่าทุกตัวใน array ให้เหลือแค่ค่าเดียว”
-->
---
hideInToc: true
---

#### Destructuring

```javascript
// Object destructuring
const user = { name: "John", age: 30 };
const { name, age } = user;
// name = 'John', age = 30

// Array destructuring
const colors = ["red", "green", "blue"];
const [primary, secondary] = colors;
// primary = 'red', secondary = 'green'
```

#### Template Literals

```javascript
const name = "John";
const greeting = `Hello, ${name}!`;
// "Hello, John!"

const multiline = `
  This is a
  multi-line
  string
`;
```
<!-- Destructuring คือวิธี “แยกค่าจาก Object หรือ Array แล้วเก็บไว้ในตัวแปรได้ง่ายขึ้น” -->
---
hideInToc: true
class: py-5
---

#### Ternary Operators

```javascript
// Instead of if/else
const age = 20;
let message;

if (age >= 18) {
  message = "Adult";
} else {
  message = "Minor";
}

// Using ternary operator
const message = age >= 18 ? "Adult" : "Minor";
```

#### ES Modules and Import/Export

```javascript
// Exporting (utils.js)
export const add = (a, b) => a + b;
export default function divide(a, b) {
  return a / b;
}

// Importing (app.js)
import divide, { add } from "./utils.js";

add(2, 3); // 5
divide(6, 2); // 3
```
