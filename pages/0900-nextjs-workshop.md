# Next.js Workshop

### 🧑‍💻 From React to building your first Next.js application

**Duration:** 1 hours

**Target Audience:** Absolute beginners with basic knowledge of HTML, CSS, and JavaScript.  
**Goal:** Build a simple multi-page Next.js application with basic authentication while learning core concepts through hands-on practice.

---
hide: true
---

## Module 1: Introduction and Setup (10 minutes)

### What is Next.js and its benefits

Next.js builds on React by adding:

- **Server-side rendering** and **Static site generation**
- **File-based routing** with the App Router
- **Server Components** for improved performance
- **Built-in optimizations** for images, fonts, and scripts
- **API Routes** for backend functionality
- **Development tools** for a better developer experience

---

## 🛠️ Development Environment (10 minutes)

- **Code Editor**: VS Code (recommended), WebStorm, Sublime Text, etc.
- **Node.js**: Version 20 or later
- **Browser**: Chrome/Edge or Firefox
- **Terminal**: Command-line access for running development commands

## Optional but Helpful

- **Browser**: Chrome or Firefox with React Developer Tools extension
- **React Basics**: Components, props, state
- **REST APIs**: Understanding HTTP methods and JSON

[//]: # "- **TypeScript**: Basics of static typing (optional but recommended)"

---

## 💻 Development Environment Setup

To get started with Next.js development:

1. **Install Node.js 20 or later**

   - Download from [nodejs.org](https://nodejs.org/)
   - Verify installation: `node -v` and `npm -v`

2. **Install Visual Studio Code (VS Code)**
   - Download from [code.visualstudio.com](https://code.visualstudio.com/)
   - Recommended extensions:
     - ESLint (a static analysis tool for JavaScript code that helps you find and fix potential errors and inconsistencies)
     - Prettier (a helpful tool that formats your code to be consistent and easy to read)
     - JavaScript and TypeScript Intellisense (builded-in)

---

## Module 1: Introduction and Setup (10 minutes)

### Setting up a new Next.js project

Use `create-next-app` to start a new project:

```bash
npx create-next-app@latest my-next-app
```

You'll be prompted with configuration options:

```
✔ Would you like to use TypeScript? … No
✔ Would you like to use ESLint? … Yes
✔ Would you like to use Tailwind CSS? … Yes
✔ Would you like to use `src/` directory? … No
✔ Would you like to use App Router? (recommended) … Yes
✔ Would you like to customize the default import alias? … No
```

---

## Module 1: Introduction and Setup

### Basic CLI commands and `package.json`

The generated `package.json` includes useful scripts:

```json {5-10}{maxHeight:'120px'}
{
  "name": "my-next-app",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint"
  },
  "dependencies": {
    "next": "14.0.0",
    "react": "^18",
    "react-dom": "^18"
  },
  "devDependencies": {
    "@types/node": "^20",
    "@types/react": "^18",
    "@types/react-dom": "^18",
    "eslint": "^8",
    "eslint-config-next": "14.0.0",
    "typescript": "^5"
  }
}
```

Common npm commands:

- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run start` - Start production server
- `npm run lint` - Run ESLint

Start the dev server with `npm run dev` and view at `http://localhost:3000`

---
hide: true
---

## Module 1: Introduction and Setup (10 minutes)

**Hands-On Practice:**

- Run `npx create-next-app@latest my-next-app`.
- Start the dev server with `npm run dev` and view at `http://localhost:3000`

---

## Module 2: Project Structure and First Page (5 minutes)

### Next.js project structure

A typical Next.js project with App Router:

```
my-next-app/
├── app/                  # App Router directory
│   ├── page.jsx          # Home page (/)
│   ├── layout.jsx        # Root layout
│   ├── globals.css       # Global styles
│   └── favicon.ico       # Favicon
├── public/               # Static assets
│   ├── images/           # Image files
│   └── fonts/            # Font files
├── components/           # Reusable components
│   ├── Button.jsx
│   └── Navbar.jsx
├── lib/                  # Utility functions
├── styles/               # Component styles
├── next.config.js        # Next.js configuration
├── package.json          # Project dependencies
└── README.md             # Project documentation
```

---

## Module 2: Project Structure and First Page

### App Router basics

In Next.js with App Router:

- Each folder represents a route segment
- The `page.jsx` file defines the UI for a route
- The `layout.jsx` file defines shared UI for multiple pages
- Files are automatically routed based on their location

---

## Module 2: Project Structure and First Page

### Creating a page

**Hands-On Practice:** Replace the default home page with your own content:

```jsx
// app/page.jsx
export default function Home() {
  return <h1>Welcome to My Next.js Site!</h1>;
}
```

---

## Module 3: Creating Pages and Navigation (5 minutes)

Create an About page by adding a new folder and page file:

```jsx
// app/about/page.jsx
export default function About() {
  return <h1>About Me</h1>;
}
```

---

## Module 3: Creating Pages and Navigation

### Navigation with `Link`

Use the `Link` component for client-side navigation between pages:

```jsx
// app/components/Header.jsx
import Link from "next/link";

export default function Header() {
  return (
    <nav>
      <Link href="/">Home</Link> | <Link href="/about">About</Link>
    </nav>
  );
}
```

---
hide: true
---

## Module 3: Creating Pages and Navigation (5 minutes)

**Hands-On Practice:**

- Create `app/about/page.jsx`:
  ```jsx
  export default function About() {
    return <h1>About Me</h1>;
  }
  ```
- Create `app/components/Header.jsx`:

  ```jsx
  import Link from "next/link";

  export default function Header() {
    return (
      <nav>
        <Link href="/">Home</Link> | <Link href="/about">About</Link>
      </nav>
    );
  }
  ```

- Import and Add `<Header />` to `app/page.jsx`.

---

## Module 4: Layouts and Shared Components (5 minutes)

### Using layouts

Layouts in Next.js allow you to share UI between multiple pages:

```jsx
// app/layout.jsx
import Header from "./components/Header";

export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body>
        <Header />
        <div className="flex flex-col h-full min-h-screen">{children}</div>
        <footer className="flex justify-center items-center h-16 bg-gray-800 text-white static bottom-0 w-full">
          <p>© 2025 My Next.js Site</p>
        </footer>
      </body>
    </html>
  );
}
```

<!--
Move <Header /> from home page to shared layout.
-->

---
hide: true
---

## Module 4: Layouts and Shared Components (5 minutes)

### Sharing components

Components can be shared across multiple pages:

- Place reusable components in a `components` folder
- Import and use them in your pages and layouts

---
hide: true
---

## Module 4: Layouts and Shared Components (5 minutes)

**Hands-On Practice:**

- Modify `app/layout.jsx`:

  ```jsx
  import Header from "./components/Header";

  export default function RootLayout({ children }) {
    return (
      <html lang="en">
        <body>
          <Header />
          <main>{children}</main>
          <footer>© 2023 My Site</footer>
        </body>
      </html>
    );
  }
  ```

---

## Module 5: Server vs. Client Components (10 minutes)

### Server vs. client components

In Next.js 13+, components are Server Components by default:

- **Server Components**: Render on the server, can't use hooks or browser APIs
- **Client Components**: Render on the client, can use React hooks and browser APIs

---

## Module 5: Server vs. Client Components

### Adding interactivity

To create a Client Component, add the `"use client"` directive at the top:

```jsx
// app/components/Header.jsx
"use client";
import Link from "next/link";
import { useState } from "react";

export default function Header() {
  const [count, setCount] = useState(0);
  return (
    <nav>
      <Link href="/">Home</Link> | <Link href="/about">About</Link>
    </nav>
    <button className="border border-amber-400 cursor-pointer" onClick={() => setCount(count + 1)}>Clicks: {count}</button>
  );
}
```

---
hide: true
---

## Module 5: Server vs. Client Components (5 minutes)

**Hands-On Practice:**

- Update `app/components/Header.jsx`:

  ```jsx
  "use client";
  import Link from "next/link";
  import { useState } from "react";

  export default function Header() {
    const [count, setCount] = useState(0);
    return (
      <nav>
        <Link href="/">Home</Link> | <Link href="/about">About</Link>
        <button onClick={() => setCount(count + 1)}>Clicks: {count}</button>
      </nav>
    );
  }
  ```

---
hide: true
---

## Module 6: Basic Styling (5 minutes)

### CSS modules

Next.js supports CSS Modules for component-level styling:

```css
/* app/components/Header.module.css */
.nav {
  padding: 10px;
  background-color: #f0f0f0;
}
```

```jsx {*}{maxHeight:'50%'}
// app/components/Header.jsx
"use client";
import Link from "next/link";
import { useState } from "react";
import styles from "./Header.module.css";

export default function Header() {
  const [count, setCount] = useState(0);
  return (
    <nav className={styles.nav}>
      <Link href="/">Home</Link> | <Link href="/about">About</Link>
      <button onClick={() => setCount(count + 1)}>Clicks: {count}</button>
    </nav>
  );
}
```

---
hide: true
---

## Module 6: Basic Styling (5 minutes)

**Hands-On Practice:**

- Create `app/components/Header.module.css`:
  ```css
  .nav {
    padding: 10px;
    background-color: #f0f0f0;
  }
  ```
- Update `app/components/Header.jsx`:
  ```jsx
  import styles from "./Header.module.css";
  // ... inside the component
  <nav className={styles.nav}>...</nav>;
  ```

---

## Module 6: Simple Authentication and Protected Routes (20 minutes)

### Login page creation

Create a simple login page with a form:

```jsx {*}{maxHeight:'70%'}
// app/login/page.jsx
"use client";
import { useState } from "react";
import { useRouter } from "next/navigation";

export default function Login() {
  const [username, setUsername] = useState("");
  const [password, setPassword] = useState("");
  const router = useRouter();

  const handleLogin = () => {
    if (username === "user" && password === "pass") {
      localStorage.setItem("token", "fake-token");
      router.push("/profile");
    } else {
      alert("Invalid credentials");
    }
  };

  return (
    <>
      <div className="flex min-h-full flex-1 flex-col justify-center px-6 lg:px-8">
        <div className="mt-10 sm:mx-auto sm:w-full sm:max-w-sm">
          <div>
            <label htmlFor="yser" className="block text-sm/6 font-medium">
              Username
            </label>
            <div className="mt-2">
              <input
                type="text"
                value={username}
                onChange={(e) => setUsername(e.target.value)}
                className="block w-full rounded-md bg-white px-3 py-1.5 text-base text-gray-900 outline-1 -outline-offset-1 outline-gray-300 placeholder:text-gray-400 focus:outline-2 focus:-outline-offset-2 focus:outline-indigo-600 sm:text-sm/6"
              />
            </div>
          </div>
          <div>
            <label htmlFor="password" className="block text-sm/6 font-medium">
              password
            </label>
            <div className="mt-2">
              <input
                type="password"
                value={password}
                onChange={(e) => setPassword(e.target.value)}
                className="block w-full rounded-md bg-white px-3 py-1.5 text-base text-gray-900 outline-1 -outline-offset-1 outline-gray-300 placeholder:text-gray-400 focus:outline-2 focus:-outline-offset-2 focus:outline-indigo-600 sm:text-sm/6"
              />
            </div>
          </div>
          <button
            type="submit"
            className="flex w-full justify-center rounded-md bg-indigo-600 px-3 py-1.5 text-sm/6 font-semibold text-white shadow-xs hover:bg-indigo-500 focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 mt-10"
            onClick={handleLogin}
          >
            Login
          </button>
        </div>
      </div>
    </>
  );
}
```

---

## Module 6: Simple Authentication and Protected Routes (5 minutes)

### Protecting routes

Create a profile page that checks for authentication:

```jsx {*}{maxHeight:'70%'}
// app/profile/page.jsx
"use client";
import { useEffect } from "react";
import { useRouter } from "next/navigation";

export default function Profile() {
    const router = useRouter();
    const token = typeof window !== "undefined" ? localStorage.getItem("token") : null;
    useEffect(() => {
        if (!token) {
            router.push("/login");
        }
    }, [token]);

    const handleLogout = () => {
        localStorage.removeItem("token");
        router.push("/login");
    };

    return (
        <>
            <div className="mt-52 mx-auto">
                <h1 className="mt-52">Hello! This is profile Page</h1>
                <button
                    type="button"
                    onClick={handleLogout}
                    className="mx-auto w-20 flex justify-center rounded-md bg-indigo-600 px-3 py-1.5 text-sm/6 font-semibold text-white shadow-xs hover:bg-indigo-500 focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 mt-10"
                >
                    Logout
                </button>
            </div>

        </>
    );
}
```

<!--
"compilerOptions": {
        "jsx": "preserve",
    },
-->

---

## Module 6: Simple Authentication and Protected Routes

Update the Header to include links to the new pages:

```jsx
// app/components/Header.jsx
"use client";
import Link from "next/link";
import { useState } from "react";

export default function Header() {
  const [count, setCount] = useState(0);

  return (
    <nav className="flex justify-start p-4 gap-5 bg-gray-800 text-white">
      <Link href="/">Home</Link> | <Link href="/about">About</Link> |{" "}
      <Link href="/login">login</Link>
      <button
        type="button"
        className="bg-blue-500 hover:bg-blue-700 text-white font-bold py-1 px-3 rounded disabled:opacity-50"
        onClick={() => setCount(count + 1)}
      >
        Click: {count}
      </button>
    </nav>
  );
}
```
