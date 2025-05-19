# Props and State Examples

Practical examples of using Props and State in React applications.

---

## Displaying Data with Props

Props allow you to pass data from parent to child components:

```jsx {*}{maxHeight:'80%',lines:true}
// Parent component
function UserList() {
  const users = [
    { id: 1, name: 'Alice', role: 'Developer' },
    { id: 2, name: 'Bob', role: 'Designer' },
    { id: 3, name: 'Charlie', role: 'Manager' }
  ];
  
  return (
    <div>
      <h2>User Directory</h2>
      {users.map(user => (
        <UserCard 
          key={user.id}
          name={user.name}
          role={user.role}
        />
      ))}
    </div>
  );
}

// Child component
function UserCard({ name, role }) {
  return (
    <div className="user-card">
      <h3>{name}</h3>
      <p>Role: {role}</p>
    </div>
  );
}
```

---

## Props: Best Practices

1. **Use destructuring** for cleaner code
2. **Provide default values** for optional props
3. **Use clear prop names** for better readability

```jsx
// Default props and destructuring example
function Button({ text = 'Click me', onClick, disabled = false }) {
  return (
    <button onClick={onClick} disabled={disabled}>
      {text}
    </button>
  );
}
```

---

## Adding Interactivity with State

State allows components to manage and update their own data:

```jsx
import { useState } from 'react';

function Counter() {
  // Initialize state with useState hook
  const [count, setCount] = useState(0);
  
  // Event handlers that update state
  const increment = () => setCount(count + 1);
  const decrement = () => setCount(count - 1);
  const reset = () => setCount(0);
  
  return (
    <div>
      <h2>Counter: {count}</h2>
      <button onClick={decrement}>-</button>
      <button onClick={reset}>Reset</button>
      <button onClick={increment}>+</button>
    </div>
  );
}
```

---
hide: true
---

## State: Form Handling Example

Using state to handle form inputs:

```jsx {*}{maxHeight:'80%',lines:true}
import { useState } from 'react';

function SignupForm() {
  const [formData, setFormData] = useState({
    username: '',
    email: '',
    password: ''
  });
  
  const handleChange = (e) => {
    const { name, value } = e.target;
    setFormData({
      ...formData,  // Keep existing form data
      [name]: value // Update only the changed field
    });
  };
  
  const handleSubmit = (e) => {
    e.preventDefault();
    console.log('Form submitted:', formData);
    // Submit to server, etc.
  };
  
  return (
    <form onSubmit={handleSubmit}>
      <div>
        <label htmlFor="username">Username:</label>
        <input
          type="text"
          id="username"
          name="username"
          value={formData.username}
          onChange={handleChange}
        />
      </div>
      
      <div>
        <label htmlFor="email">Email:</label>
        <input
          type="email"
          id="email"
          name="email"
          value={formData.email}
          onChange={handleChange}
        />
      </div>
      
      <div>
        <label htmlFor="password">Password:</label>
        <input
          type="password"
          id="password"
          name="password"
          value={formData.password}
          onChange={handleChange}
        />
      </div>
      
      <button type="submit">Sign Up</button>
    </form>
  );
}
```

---

## State: Conditional Rendering

Using state to conditionally render UI elements:

```jsx {*}{maxHeight:'80%',lines:true}
import { useState } from 'react';

function ToggleContent() {
  const [isVisible, setIsVisible] = useState(false);
  
  return (
    <div>
      <button onClick={() => setIsVisible(!isVisible)}>
        {isVisible ? 'Hide Details' : 'Show Details'}
      </button>
      
      {isVisible && (
        <div className="details">
          <p>These are the additional details that can be shown or hidden.</p>
          <ul>
            <li>Detail 1</li>
            <li>Detail 2</li>
            <li>Detail 3</li>
          </ul>
        </div>
      )}
    </div>
  );
}
```

---
hide: true
---

## Combining Props and State

A component that uses both props and state:

```jsx {*}{maxHeight:'80%',lines:true}
import { useState } from 'react';

// Parent component with state
function ProductPage() {
  const [cart, setCart] = useState([]);
  
  const addToCart = (product) => {
    setCart([...cart, product]);
  };
  
  const products = [
    { id: 1, name: 'Laptop', price: 999 },
    { id: 2, name: 'Phone', price: 699 },
    { id: 3, name: 'Tablet', price: 399 }
  ];
  
  return (
    <div>
      <h1>Products</h1>
      <div className="product-list">
        {products.map(product => (
          <ProductCard 
            key={product.id}
            product={product}
            onAddToCart={addToCart}
          />
        ))}
      </div>
      
      <div className="cart">
        <h2>Cart ({cart.length} items)</h2>
        <ul>
          {cart.map((item, index) => (
            <li key={index}>{item.name} - ${item.price}</li>
          ))}
        </ul>
      </div>
    </div>
  );
}

// Child component with its own state
function ProductCard({ product, onAddToCart }) {
  const [isHovered, setIsHovered] = useState(false);
  
  return (
    <div 
      className={`product-card ${isHovered ? 'hovered' : ''}`}
      onMouseEnter={() => setIsHovered(true)}
      onMouseLeave={() => setIsHovered(false)}
    >
      <h3>{product.name}</h3>
      <p>${product.price}</p>
      <button onClick={() => onAddToCart(product)}>
        Add to Cart
      </button>
    </div>
  );
}
```

---
hide: true
---

## State Management Beyond useState

For more complex applications, consider:

1. **useReducer**: For complex state logic
2. **Context API**: For sharing state across components
3. **State management libraries**:
   - Redux
   - MobX
   - Zustand
   - Recoil
   - Jotai

These solutions help manage application state as it grows in complexity.
