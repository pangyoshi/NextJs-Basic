# ReactJS vs. Next.js

Key differences and when to use each framework

---
hide: true
---
## React: The Library

React is a JavaScript library for building user interfaces:

- **Focus**: UI components
- **Rendering**: Client-side by default
- **Routing**: Requires additional libraries (React Router)
- **Data Fetching**: No built-in solution
- **Bundling/Build**: Requires setup (Create React App, Webpack, etc.)
- **Deployment**: More configuration needed

---
hide: true
---
## Next.js: The Framework

Next.js is a complete React framework:

- **Focus**: Full-stack applications
- **Rendering**: Server-side, static, and client-side
- **Routing**: Built-in file-based routing
- **Data Fetching**: Built-in data fetching methods
- **Bundling/Build**: Zero configuration
- **Deployment**: Optimized for Vercel, but works anywhere

---

## ⚛️ Rendering Comparison

### React (Client-Side Rendering)
```jsx
// All rendering happens in the browser
function App() {
  const [data, setData] = React.useState(null);

  React.useEffect(() => {
    fetch('/api/data')
      .then(res => res.json())
      .then(data => setData(data));
  }, []);

  if (!data) return <div>Loading...</div>;

  return <div>{data.title}</div>;
}
```

---

## ⏩ Rendering Comparison (continued)

### Next.js (Server-Side Rendering)
```jsx
// app/page.jsx
// Server Components can fetch data directly
async function Page() {
  // This code runs on the server
  const res = await fetch('https://api.example.com/data');
  const data = await res.json();

  return <div>{data.title}</div>;
}

export default Page;
```

---

## Routing Comparison

### React with React Router
```jsx
// App.js
import { BrowserRouter, Routes, Route } from 'react-router-dom';

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/blog/:id" element={<BlogPost />} />
      </Routes>
    </BrowserRouter>
  );
}
```

---

## 📂 Routing Comparison (continued)

### Next.js File-Based Routing
```
app/
├── page.jsx         // Route: /
├── about/
│   └── page.jsx     // Route: /about
└── blog/
    └── [id]/
        └── page.jsx // Route: /blog/:id
```

```jsx
// app/blog/[id]/page.jsx
function BlogPost({ params }) {
  // params are provided by Next.js
  const { id } = React.use(params);

  return <div>Blog Post: {id}</div>;
}

export default BlogPost;
```

---

## Data Fetching Comparison

### React
```jsx
function ProductList() {
  const [products, setProducts] = React.useState([]);
  const [loading, setLoading] = React.useState(true);

  React.useEffect(() => {
    fetch('/api/products')
      .then(res => res.json())
      .then(data => {
        setProducts(data);
        setLoading(false);
      });
  }, []);

  if (loading) return <div>Loading...</div>;

  return (
    <ul>
      {products.map(product => (
        <li key={product.id}>{product.name}</li>
      ))}
    </ul>
  );
}
```

---

## Data Fetching Comparison (continued)

### Next.js
```jsx
// app/products/page.jsx
// Static Site Generation (SSG) with App Router
async function ProductList() {
  // fetch with revalidate option for Incremental Static Regeneration (ISR)
  const res = await fetch('https://api.example.com/products', {
    next: { revalidate: 60 } // Regenerate page every 60 seconds
  });
  const products = await res.json();

  return (
    <ul>
      {products.map(product => (
        <li key={product.id}>{product.name}</li>
      ))}
    </ul>
  );
}

export default ProductList;
```

---

## React vs Next.js — At a Glance

| React (Library) | Next.js (Framework) |
|------------------|---------------------|
| UI Components Only | Full-Stack Web Applications |
| Client-side Only | SSR, SSG, ISR, Client-side |
| Manual setup (e.g., React Router) | Built-in File-based Routing |
| No Built-in Solution | Built-in Methods (getServerSideProps, etc.) |
| Needs Configuration (CRA, Webpack) | Zero Config Out of the Box |
| Manual Setup Required | Optimized for Vercel, Works Anywhere |
---

## When to Choose React vs Next.js?

| Choose React When | Choose Next.js When |
|------------------|---------------------|
| Building highly interactive single-page applications | Building production websites that need SEO |
| Working within existing React applications | Need server-side rendering or static site generation |
| Need complete control over application architecture | Want built-in routing, API routes, and image optimization |
| Want specific routing or state management solutions | Need faster initial page loads |
| Building libraries or components for various projects | Building full-stack applications with React |
| Working with specialized build systems | Want zero-config development environment |
| | Need to scale your application easily |
