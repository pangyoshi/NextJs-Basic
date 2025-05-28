# What is Next.js?

Next.js is a React framework that provides structure, features, and optimizations for your application.

<img src="/assets/nextjs.png" class="mt-5 w-[50%] mx-auto" />

---
layout: two-cols
---
## ⏩ Why Next.js?

Next.js extends React with:

- **Server-side rendering**
- **Static site generation**
- **File-based routing**
- **API routes**
- **Built-in CSS and Sass support**
- **Code splitting and bundling**
- **Image optimization**
- **Development environment with Fast Refresh**

::right::
<img src="/assets/why-nextjs.png" class="mt-5 w-[100%] mx-auto" />

<!--
SSG = สร้างไว้ล่วงหน้าตอน Build → โหลดเร็ว ใช้กับข้อมูลคงที่ เช่น ข้อมูลติดต่อเรา, เกี่ยวกับริษัทเรา, ที่อยู่

SSR = สร้างหน้าเว็บ ตอนที่ผู้ใช้เข้ามา โดยดึงข้อมูลจาก server → เหมาะกับข้อมูลเปลี่ยนบ่อย

API routes คือการสร้าง Back-end API ง่าย ๆ ภายใน Next.js
โดยไม่ต้องตั้ง Server แยกเอง
-->

---

## 🛢️ Server-Side Rendering (SSR)

Next.js can render React components on the server before sending to the client:

<img src="/assets/single-page-app.webp" class="mt-5 w-[75%] mx-auto" />

<!--
การที่ เว็บเพจถูกสร้างบนเซิร์ฟเวอร์ แล้วส่งหน้า HTML ที่ 'เสร็จสมบูรณ์' ไปให้ browser ทันที

ต่างจากแบบปกติ (เช่น React ทั่วไป) ที่โหลดหน้าเว็บ → แล้วค่อยใช้ JavaScript สร้างเนื้อหาในฝั่ง browser
-->

---
hide: true
---

## 🛢️ Server-Side Rendering (SSR)

Next.js can render React components on the server before sending to the client:

```jsx
// app/page.jsx
async function HomePage() {
  // Fetch data directly in the component (Server Component)
  const res = await fetch("https://api.example.com/data");
  const data = await res.json();

  return <div>{data.title}</div>;
}

export default HomePage;
```

---

## 🧾 Static Site Generation (SSG)

Pre-render pages at build time for better performance:
<img src="/assets/static-site-generation.png" class="mt-5 w-[75%] mx-auto" />

<!--
SSG คือการ สร้างหน้า HTML ล่วงหน้า ตั้งแต่ตอน build

เวลา user เข้าหน้าเว็บ → เว็บโหลดทันที เพราะทุกอย่างถูกสร้างไว้แล้ว

ไม่ต้องรอ fetch ข้อมูล → ไม่ต้องรอรัน JavaScript → เร็วสุดๆ

เหมือนกับ...
🧁 SSG = เราอบเค้กเตรียมไว้ล่วงหน้าในร้าน → ลูกค้ามาถึงก็เสิร์ฟได้ทันที
🧑‍🍳 SSR = ลูกค้าสั่งก่อน แล้วค่อยอบเค้กเสิร์ฟตามออเดอร์
-->

---
hide: true
---
## 🧾 Static Site Generation (SSG)

Pre-render pages at build time for better performance:

```jsx
// app/blog/[slug]/page.jsx
export async function generateStaticParams() {
  // Return a list of possible values for slug
  return [{ slug: "hello-world" }, { slug: "learn-nextjs" }];
}

async function BlogPost({ params }) {
  // Fetch data based on slug
  const res = await fetch(`https://api.example.com/posts/${params.slug}`);
  const post = await res.json();

  return <div>{post.title}</div>;
}

export default BlogPost;
```

---

## 📂 File-Based Routing (App Router)

Next.js creates routes based on the file system:

```
app/
├── page.jsx               // Route: / (Home page)
├── layout.jsx             // Root layout (applies to all routes)
├── about/
│   └── page.jsx           // Route: /about
├── blog/
│   ├── page.jsx           // Route: /blog
│   └── [slug]/
│       └── page.jsx       // Route: /blog/:slug
└── api/
    └── hello/
        └── route.js       // API Route: /api/hello
```

The App Router uses a convention where:

- `page.jsx` defines a route
- `layout.jsx` defines a shared layout
- `loading.jsx` creates loading UI
- `error.jsx` handles errors
- `route.js` creates API endpoints

---

## 🚀 API Routes (Route Handlers)

Create API endpoints as Route Handlers:

```jsx
// app/api/hello/route.js
export async function GET() {
  return Response.json({ name: "John Doe" });
}

export async function POST(request) {
  const data = await request.json();
  // Process the data
  return Response.json({ received: data });
}
```

Access with:

```javascript
// Client-side
fetch("/api/hello")
  .then((res) => res.json())
  .then((data) => console.log(data));
```

<!--
เรายังสามารถสร้าง API ได้ภายในโปรเจกต์เดียวกัน โดยไม่ต้องมีเซิร์ฟเวอร์แยก!"

เขียนเหมือนทำ route ปกติ → แต่เอาไว้ตอบข้อมูล ไม่ใช่ render หน้า

เหมือนกับ...
🔌 API Route = ช่องเชื่อมต่อข้อมูลระหว่าง frontend ↔ backend
🗃️ เราส่ง request ไป → Route ตอบกลับด้วยข้อมูล JSON
-->

---
hide: true
---

## Built-in CSS Support

Next.js supports various styling options:

```jsx {*}{maxHeight:'80%'}
// CSS Modules
import styles from "./Button.module.css";

function Button() {
  return <button className={styles.button}>Click me</button>;
}

// Global CSS
import "../styles/globals.css";

// Styled JSX (CSS-in-JS)
function Button() {
  return (
    <>
      <button>Click me</button>
      <style jsx>{`
        button {
          background: blue;
          color: white;
        }
      `}</style>
    </>
  );
}
```

---

## 🖼️ Image Optimization

Next.js optimizes images automatically:

```jsx
import Image from "next/image";

function Avatar() {
  return (
    <Image
      src="/profile.jpg"
      alt="Profile picture"
      width={500}
      height={500}
      priority
    />
  );
}
```

#### Benefits:

- Automatic WebP/AVIF conversion
- Responsive sizes
- Lazy loading
- Prevents layout shift

---
hide: true
---

## Development Experience

Next.js provides an excellent developer experience:

- **Fast Refresh**: See changes instantly without losing component state
- **TypeScript Support**: Built-in TypeScript configuration
- **ESLint Integration**: Catch errors early
- **Detailed Error Reporting**: Clear error messages with suggestions
- **Analytics**: Built-in performance metrics
