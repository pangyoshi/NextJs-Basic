---
layout: two-cols-header
layoutClass: gap-x-4 gap-y-2
hide: true
---

# Imperative vs. declarative programming

::left::

### **Imperative** (Vanilla JS):

<p class="h-12">
You manually update the DOM step-by-step:
</p>

```javascript
const button = document.createElement('button');
button.textContent = 'Click me: 0';
let count = 0;

button.addEventListener('click', () => {
  count++;
  button.textContent = `Click me: ${count}`;
  // Explicitly update the DOM
});

document.body.appendChild(button);
```

::right::

### **Declarative** (React):

<p class="h-12">
You describe the UI based on state, and React handles updates:
</p>

```javascript
function App() {
  const [count, setCount] = React.useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      Click me: {count}
    </button>
  );
}

ReactDOM.render(<App />, document.body);
```

::bottom::

### **Key Difference**:
- **Imperative**: You directly manipulate the DOM (e.g., `button.textContent = ...`).
- **Declarative**: React updates the DOM *for you* based on state changes (`count`).
<!-- may remove all -->