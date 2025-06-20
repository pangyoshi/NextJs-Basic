<!-- # Getting Ready for Next.js -->
# Getting Ready for Next.js

Essential Web Fundamentals You Should Know Before diving into Next.js, you should be familiar with:

- **🧾 HTML**: Basic structure, elements, attributes, and forms
- **🎨 CSS**: Selectors, properties, layouts (Flexbox/Grid), responsive design
- **⚙️ JavaScript**: ES6+ features, including:
  - Arrow functions
  - Template Literals
  - Ternary Operators
  - Destructuring
  <!-- - Spread/rest operators -->
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

<!--
- คือการดึงข้อมูลจากแหล่งอื่น เช่น API หรือฐานข้อมูล เพื่อแสดงข้อมูลแบบเรียลไทม์หรืออัปเดตให้ผู้ใช้เห็น
- State คือข้อมูลภายในแอป เช่น สถานะของปุ่มหรือรายการในรถเข็น เราต้องจัดการ state ให้ดีเพื่อให้แอปทำงานลื่นไหล
- Authentication คือการยืนยันตัวตนของผู้ใช้ เช่น การล็อกอิน เพื่อให้รู้ว่าใครกำลังใช้งานระบบอยู่
- การป้องกันการโจมตีและดูแลข้อมูลไม่ให้รั่วไหล
ทั้งหมดนี้คือสิ่งที่เราจะใช้ในการสร้างเว็บแอปที่ทันสมัย มีคุณภาพ
-->

---
level: 1
---

# Single Page Applications (SPAs) - React, Vue, ...

## ⚡What is a SPA?

A Single Page Application (SPA) is a web application that loads a single HTML page and dynamically updates the content as the user interacts with the app, without reloading the entire page.

<img src="/assets/single-page-app.webp" class="mt-5 w-[75%] mx-auto" />

<!--
เวลาเราเข้าเว็บไซต์ทั่วไปแบบดั่งเดิม เราคลิกลิงก์แต่ละครั้ง หน้าเว็บจะโหลดใหม่ทั้งหน้า — เหมือนเรากำลังเปลี่ยนหน้าหนังสือจริง ๆ
แต่ใน Single Page Application หรือ SPA เมื่อเราคลิกเปลี่ยนหน้า ระบบจะไม่โหลดหน้าเว็บใหม่ทั้งหมด แต่จะโหลดเฉพาะข้อมูลที่เปลี่ยนผ่าน JavaScript
-->

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

<!--
เมื่อผู้ใช้โต้ตอบกับเว็บ เช่น คลิกปุ่มหรือกรอกแบบฟอร์ม ตัวเว็บจะอัปเดตแค่ส่วนที่เปลี่ยน ไม่โหลดทั้งหน้าใหม่
ตัวอย่าง: กด "เพิ่มสินค้าในรถเข็น" แล้วเห็นยอดรวมเปลี่ยนทันที โดยที่หน้าอื่นไม่หาย

เว็บแอปสมัยใหม่ทำงานลื่นไหลและตอบสนองเร็ว คล้ายแอปที่เราใช้บนคอม
ตัวอย่าง: ใช้ Gmail หรือ Google Docs เราพิมพ์หรือคลิกแล้วทุกอย่างเปลี่ยนทันที ไม่ต้องรีเฟรชหน้า
-->

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

<!--
!------------- BREAK -------------!

- ไม่ต้องโหลดหน้าซ้ำให้สะดุด
- เว็บตอบสนองเร็วขึ้น เพราะส่งแค่ข้อมูลที่เปลี่ยน
- ระหว่างโหลดข้อมูล หน้าเว็บยังใช้งานได้ ไม่ค้างหรือหยุดตอบสนอง ตัวอย่าง: เวลาโพสต์คอมเมนต์ แอปอาจขึ้น “กำลังส่ง...” แต่เรายังเลื่อนดูโพสต์อื่นได้
- บางเว็บสามารถทำงานต่อได้แม้ไม่มีอินเทอร์เน็ต เช่น บันทึกข้อมูลไว้แล้วส่งเมื่อออนไลน์อีกครั้ง
ตัวอย่าง: แอปจดโน้ตอย่าง Notion หรือ Google Keep สามารถเขียนโน้ตแบบออฟไลน์ แล้วซิงก์ทีหลัง

insert more images Ex. App
-->

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

<!--
Object คือ กล่องที่เก็บข้อมูลหลายอย่าง ในรูปแบบ (key - value)
ในที่นี้เหมือนแฟ้มข้อมูลของคนหนึ่งคน
.map(): เปลี่ยนค่าทุกตัวใน array 
จะได้จำนวนผลลัพธ์เท่าเดิม =>	Array ใหม่
.filter(): คัดเฉพาะตัวที่ "ผ่านเงื่อนไข" => Array ใหม่ที่สั้นลง
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
console.log("Hello, " + name + "!");

const greeting = `Hello, ${name}!`;
// "Hello, John!"

const multiline = `
  This is a
  multi-line
  string
`;
```

<!--
Destructuring คือวิธี “แยกค่าจาก Object หรือ Array แล้วเก็บไว้ในตัวแปรได้ง่ายขึ้น”

“ปกติเวลาที่เราต้องการเชื่อมข้อความกับตัวแปรใน JavaScript แบบง่ายๆ เรามักจะใช้ + ในการต่อข้อความ เช่น…”

“Template Literals ทำให้เราเขียนข้อความที่มีตัวแปรแทรกอยู่ โดยใช้เครื่องหมาย backtick ` แทน double quote และใช้ ${} เพื่อใส่ตัวแปรข้างในได้เลย”
-->

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
// condition ? true : false
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

<!--
Ternary Operator เป็นวิธีเขียนเงื่อนไขแบบสั้น แทนการใช้ if-else แบบยาว
มันเหมาะกับกรณีที่เราต้องการเช็คบางอย่าง แล้วแสดงผลลัพธ์แบบสองทาง เช่น ‘ถ้าใช่ ให้แสดง A ถ้าไม่ใช่ ให้แสดง B
-->
