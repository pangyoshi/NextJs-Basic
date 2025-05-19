# What is the DOM?

The Document Object Model (DOM) is a programming interface for web documents.

---

## The DOM as a Tree

The DOM represents an HTML document as a tree structure:

```
Document
└── html
    ├── head
    │   ├── title
    │   │   └── "My Page"
    │   └── meta
    └── body
        ├── h1
        │   └── "Hello World"
        ├── p
        │   └── "This is a paragraph"
        └── div
            └── button
                └── "Click me"
```

---

## HTML

HTML is the **text** representation of a web page:

```html
<!DOCTYPE html>
<html>
<head>
  <title>My Page</title>
  <meta charset="UTF-8">
</head>
<body>
  <h1>Hello World</h1>
  <p>This is a paragraph</p>
  <div>
    <button>Click me</button>
  </div>
</body>
</html>
```

---
layout: two-cols-header
---

## HTML vs. the DOM (continued)

The DOM is the **object** representation of the HTML:

<img src="/assets/dom-tree.webp" class="mt-5 w-3/2 h-100 mx-auto" />

---

## Key Differences

| HTML | DOM |
|------|-----|
| Static text/markup | Live, dynamic object structure |
| Written by developers | Created by the browser |
| Doesn't change | Can be modified by JavaScript |
| Describes initial structure | Represents current state |
| File-based | In-memory representation |

---
hide: true
---

## The DOM API

JavaScript can interact with the DOM through various methods:

```javascript
// Creating elements
const newParagraph = document.createElement('p');
newParagraph.textContent = 'This is a new paragraph';
document.body.appendChild(newParagraph);

// Selecting elements
const elements = document.querySelectorAll('.item');
const firstElement = document.getElementById('first');

// Modifying elements
firstElement.classList.add('highlighted');
firstElement.setAttribute('data-status', 'active');

// Handling events
firstElement.addEventListener('click', handleClick);
```
<!-- may remove -->
---
hide: true
---

## DOM Manipulation is Expensive

Directly manipulating the DOM can be slow:

```javascript
// Inefficient: Multiple DOM operations
for (let i = 0; i < 1000; i++) {
  const item = document.createElement('li');
  item.textContent = `Item ${i}`;
  document.getElementById('list').appendChild(item);
}

// More efficient: Single DOM operation
const fragment = document.createDocumentFragment();
for (let i = 0; i < 1000; i++) {
  const item = document.createElement('li');
  item.textContent = `Item ${i}`;
  fragment.appendChild(item);
}
document.getElementById('list').appendChild(fragment);
```
<!-- may remove -->
---

## The DOM and React

React uses a Virtual DOM to minimize direct DOM manipulation:

1. **HTML**: The initial markup
2. **DOM**: Browser's object representation
3. **Virtual DOM**: React's lightweight copy of the DOM
4. **Reconciliation**: React's process for updating the DOM efficiently

This approach makes React applications faster and more efficient.