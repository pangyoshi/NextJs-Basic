# What is JSX?

JSX (JavaScript XML) is a syntax extension for JavaScript that looks similar to HTML but allows you to write HTML-like code in JavaScript.

---

## 📝 JSX Basics

JSX combines JavaScript and HTML-like syntax:

```jsx
const element = <h1>Hello, world!</h1>;
```

This is neither a string nor HTML - it's JSX that gets transformed into JavaScript.

---

## HTML vs. JSX: Syntax

HTML:
```html
<div class="container">
  <p>Hello, world!</p>
  <button onclick="handleClick()">Click me</button>
</div>
```

JSX:
```jsx
<div className="container">
  <p>Hello, world!</p>
  <button onClick={handleClick}>Click me</button>
</div>
```

---

##  🔑 Key Differences: Attributes

| HTML | JSX |
|------|-----|
| `class` | `className` |
| `for` | `htmlFor` |
| `onclick` | `onClick` |
| `style="color: red;"` | `style={{ color: 'red' }}` |

JSX uses camelCase for attribute names (following JavaScript conventions).

<img src="/assets/CamelCase.png" class="mt-5 w-[25%] mx-auto" />


---
hide: true
---

## Embedding Expressions in JSX

JSX allows you to embed any JavaScript expression using curly braces:

```jsx
const name = 'John Doe';
const element = <h1>Hello, {name}!</h1>;

// Expressions
const element = <h1>2 + 2 = {2 + 2}</h1>;

// Function calls
const element = <h1>Welcome, {formatName(user)}!</h1>;

```

---
hide: true
---
## Conditional Rendering in JSX

Using JavaScript expressions for conditional rendering:

```jsx
// Ternary operator
<div>
  {isLoggedIn ? <UserGreeting /> : <GuestGreeting />}
</div>

// Logical && operator
<div>
  {unreadMessages.length > 0 &&
    <p>You have {unreadMessages.length} unread messages.</p>
  }
</div>

// Immediately-invoked function expressions (IIFE)
<div>
  {(() => {
    if (status === 'loading') return <Loading />;
    if (status === 'error') return <Error />;
    return <Data />;
  })()}
</div>
```

---
hide: true
---

## Lists in JSX

Rendering lists using map():

```jsx
const numbers = [1, 2, 3, 4, 5];

const listItems = numbers.map(number => 
  <li key={number.toString()}>
    {number}
  </li>
);

const element = <ul>{listItems}</ul>;
```

The `key` attribute helps React identify which items have changed.

---

## JSX and HTML Differences: Self-closing Tags

HTML allows unclosed tags for some elements:
```html
<input type="text">
<br>
<img src="image.jpg">
```

JSX requires all tags to be closed:
```jsx
<input type="text" />
<br />
<img src="image.jpg" />
```

---

## JSX and HTML Differences: Fragments

In HTML, you can have multiple root elements:
```html
<h1>Title</h1>
<p>Paragraph</p>
```

In JSX, you need a single root element or use fragments:
```jsx
// Using a wrapper div
<div>
  <h1>Title</h1>
  <p>Paragraph</p>
</div>

// Using React Fragment
<>
  <h1>Title</h1>
  <p>Paragraph</p>
</>

// Explicit Fragment syntax
<React.Fragment>
  <h1>Title</h1>
  <p>Paragraph</p>
</React.Fragment>
```

<!--
JSX ไม่อนุญาตให้มีหลาย root elements
คิดง่ายๆ ว่า React ต้องให้เราห่อของทั้งหมดในกล่องเดียว (เหมือนใส่ของลงในกล่องพัสดุ)
ถ้าเราไม่อยากใช้กล่องจริง (เช่น div) เราใช้กล่องล่องหน (React Fragment) แทน
แบบนี้เราก็จัดของได้โดยไม่เพิ่มน้ำหนักหรือขนาดเกินจำเป็นครับ
-->

---
hide: true
---
## JSX Behind the Scenes

JSX gets transformed into JavaScript by tools like Babel:
<!-- may cut it -->
JSX:
```jsx
const element = <h1 className="greeting">Hello, world!</h1>;
```

Transformed JavaScript:
```javascript
const element = React.createElement(
  'h1',
  { className: 'greeting' },
  'Hello, world!'
);
```

This creates a JavaScript object (Virtual DOM element).

<!--
may cut it
-->
