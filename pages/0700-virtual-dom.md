# Virtual DOM

The Virtual DOM is a key concept that makes React efficient and performant.

<img src="/assets/react-dom.jpg" class="mt-5 w-[80%] mx-auto" />

---

## What is the Virtual DOM?

The Virtual DOM is:

- A lightweight JavaScript representation of the actual DOM
- A tree of JavaScript objects that mirrors the real DOM structure
- An abstraction layer between your code and the actual DOM
- Much faster to manipulate than the real DOM

<!--
Virtual DOM คือโครงสร้างจำลองของ DOM ที่เขียนด้วย JavaScript
มันเปรียบเสมือน “ภาพร่าง” ของหน้าเว็บ ที่ React ใช้เพื่อเปรียบเทียบและอัปเดตเฉพาะส่วนที่เปลี่ยนแปลง
ทำให้การปรับ UI เร็วและมีประสิทธิภาพกว่าการแก้ไข DOM จริงโดยตรง
-->

---
hide: true
---
## The Problem with Direct DOM Manipulation

Directly manipulating the DOM is slow:

1. DOM operations cause browser reflows and repaints
2. Each update can trigger layout recalculations
3. Multiple updates create performance bottlenecks

```javascript
// Direct DOM manipulation (slow for multiple updates)
document.getElementById('counter').textContent = count;
document.getElementById('status').className = count > 10 ? 'high' : 'low';
document.getElementById('message').textContent = `Count: ${count}`;
```
<!-- may cut it -->

---
hide: true
---

## React's Solution: Virtual DOM

React's approach to DOM updates:

1. Maintain a virtual representation of the UI in memory
2. When state changes, create a new virtual DOM tree
3. Compare the new virtual tree with the previous one (diffing)
4. Calculate the minimal set of changes needed (reconciliation)
5. Apply only those changes to the real DOM (batched updates)

---

## 🧠	How React Updates the UI 

The React rendering process:

```
State/Props Change
       ↓
Render Virtual DOM
       ↓
Diff with Previous Virtual DOM
       ↓
Calculate Minimal DOM Operations
       ↓
Update Real DOM (only what changed)
```

---
hide: true
---

## Reconciliation Algorithm

React's reconciliation process follows these principles:

1. **Different element types** produce different trees
2. **List elements** with keys maintain identity across renders
3. **Same element types** preserve the DOM node, only updating changed attributes

```jsx
// Before update
<div className="container">
  <h1>Hello, World</h1>
  <p>Count: 5</p>
</div>

// After update (only p element changes)
<div className="container">
  <h1>Hello, World</h1>
  <p>Count: 6</p>
</div>
```

---

## 🔑 Keys in Lists

The `key` attribute helps React identify which items have changed, been added, or removed:

```jsx
// Without keys (inefficient)
<ul>
  {items.map(item => (
    <li>{item.text}</li>
  ))}
</ul>

// With keys (efficient)
<ul>
  {items.map(item => (
    <li key={item.id}>{item.text}</li>
  ))}
</ul>
```

<!--
"เวลาเราใช้ React สร้างรายการหลายๆ ชิ้น เช่น รายการสินค้าหรือรายชื่อคน
React จะต้อง รู้ว่ารายการไหนเปลี่ยน รายการไหนเพิ่ม หรือถูกลบออก
เพราะ React ไม่ได้ render ทั้งหมดใหม่ แต่จะพยายามอัปเดตเฉพาะส่วนที่เปลี่ยน — เพื่อให้เร็วขึ้น

เราจึงใช้สิ่งที่เรียกว่า key ซึ่งเป็น รหัสเฉพาะของแต่ละ item
เพื่อแยกแยะ
-->

---
hide: true
---
## Batching Updates

React batches multiple state updates into a single re-render for better performance:

```jsx
function handleClick() {
  // These state updates are batched into a single render
  setCount(count + 1);
  setStatus('active');
  setLastUpdated(new Date());
}
```
<!-- ใน React 18+ ฉลาดพอที่จะรวมหลาย การเปลี่ยนแปลงนี้ไว้ใน "batch" แล้ว render แค่ ครั้งเดียว -->
---
hide: true
---

## React Fiber

React Fiber is React's reconciliation engine introduced in React 16:

- **Incremental rendering**: Split rendering work into chunks
- **Priority levels**: Prioritize updates based on importance
- **Pause and resume**: Ability to pause work and come back later
- **Abort rendering**: Cancel unnecessary updates
- **Error boundaries**: Better error handling
<!-- may cut it -->
---
hide: true
---
## Performance Benefits

The Virtual DOM approach provides several benefits:

1. **Efficiency**: Minimizes actual DOM operations
2. **Abstraction**: Developers don't need to manually optimize DOM updates
3. **Declarative API**: Describe what the UI should look like, not how to change it
4. **Cross-platform**: Same approach works for web, mobile (React Native), and other platforms
