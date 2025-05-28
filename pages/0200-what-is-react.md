# What is React?

React is a JavaScript library for building user interfaces, particularly single-page applications.
<img src="/assets/react-js-ani.gif" class="mt-10 w-[75%] mx-auto w-100" />

---

## Core Concepts of React

React is built around three fundamental concepts:

1. **Components**
2. **Props**
3. **State**

---

## 🧩 Components

Components are reusable, self-contained pieces of code that return HTML via a render function.

```jsx
// Function Component
function Greeting() {
  return <h1>Hello, World!</h1>;
}

// ใช้งานใน React:
<Greeting />

```

React Component 👉 Returns JSX (HTML-like) for use in building web page UI.

---
hideInToc: true
---

## 🧩 Components (continued)

Components can be composed together to build complex UIs:

```jsx
function App() {
  return (
    <div>
      <Header />
      <MainContent />
      <Sidebar />
      <Footer />
    </div>
  );
}
```

React Component 👉 Use 𝗣𝗮𝘀𝗰𝗮𝗹 𝗖𝗮𝘀𝗲 where each word in a variable name starts with a capital letter
<!--
Pascal case สำหรับ components
-->

---

## 🎁 Props 

Props (short for "properties") are read-only inputs to components:

```jsx
// Defining a component that accepts props
function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}

// Using the component with props
<Greeting name="John" />  // Renders: Hello, John!
```

<!--
Props ทำหน้าที่เหมือน 'กล่องข้อมูล' ที่เราส่งไปให้ Component ลูก
Component ลูกจะ ‘อ่าน’ ข้อมูลจาก props เท่านั้น — ไม่สามารถแก้ไข props ได้
เพราะ props เป็น read-only หรือ ‘อ่านได้อย่างเดียว’ เพื่อให้ข้อมูลปลอดภัยและควบคุมง่าย”
-->

---
hideInToc: true
---

## 🎁 Props (continued)

Props can be destructured for cleaner code:

```jsx
function UserProfile({ name, role, avatar }) {
  return (
    <div>
      <img src={avatar} alt={name} />
      <h2>{name}</h2>
      <p>Role: {role}</p>
    </div>
  );
}

<UserProfile 
  name="Jane Doe" 
  role="Developer" 
  avatar="/images/jane.png" 
/>
```

---

## 🔁 State

State is private data controlled by a component that can change over time:

```jsx
function Counter() {
  // useState returns a state variable and a function to update it
  const [count, setCount] = React.useState(0);
  
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

<!--
State คือ ข้อมูลภายในของ Component ที่สามารถเปลี่ยนแปลงได้เมื่อมีการโต้ตอบ เช่น คลิกปุ่ม หรือพิมพ์ข้อความ

ลองนึกว่า Component คือตัวละครในเกม
และ state คือ ค่าพลังชีวิต หรือ คะแนน — ที่เปลี่ยนได้ตลอดเวลา
ถ้ามีการเปลี่ยนแปลงค่า state → React จะ re-render หน้าจอใหม่ให้เราอัตโนมัติ”
-->

---
hideInToc: true
hide: true
---

## 🔁 State (continued)

State updates trigger re-renders:

```jsx
function ToggleButton() {
  const [isOn, setIsOn] = React.useState(false);
  
  const toggle = () => {
    setIsOn(prevState => !prevState);
  };
  
  return (
    <button onClick={toggle}>
      {isOn ? 'ON' : 'OFF'}
    </button>
  );
}
```
<!-- duplicate not necessary -->
---
layout: two-cols-header
layoutClass: gap-4
hide: true
---

# React's Unidirectional Data Flow

::left::

In React, data flows in one direction:
- Props flow down from parent to child
- Events flow up from child to parent

<img src="/assets/react-data-flow.jpg" class="mt-5 me-5" />

::right::

```jsx
function Parent() {
  const [message, setMessage] = React.useState('Hello');
  
  return (
    <div>
      <h1>{message}</h1>
      <Child onMessageChange={setMessage} />
    </div>
  );
}

function Child({ onMessageChange }) {
  return (
    <button onClick={() => onMessageChange('Goodbye')}>
      Change Message
    </button>
  );
}
```
