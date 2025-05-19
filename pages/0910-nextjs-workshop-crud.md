# Next.js Workshop (Class 2): Building a CRUD Application

From basic Next.js to creating a full CRUD application

**Duration:** 1 hours 30 mins
 
**Target Audience:** Developers with basic Next.js knowledge (completed Class 1)  
**Goal:** Build a complete CRUD (Create, Read, Update, Delete) application with Next.js using a REST API.

---

## 🌐 What is a REST API?
A REST API (Representational State Transfer) is a way for applications to communicate over the web using HTTP requests.<br>

**📌Key Concepts:** <br>
Client–Server: The client (e.g. browser, app) makes requests; the server responds with data.

- GET     - Read data
- POST    - Create data
- PUT     - Update data
- DELETE  - Delete data

Example
```
GET https://api.example.com/users/1
```
→ Respone
```
{
  "id": 1,
  "name": "Alice"
}
```

---

## Module 1: Introduction to CRUD Applications

### What is CRUD?

CRUD stands for:
- **C**reate: Adding new data
- **R**ead: Retrieving and displaying data
- **U**pdate: Modifying existing data
- **D**elete: Removing data

These four operations form the foundation of most web applications that manage data.

---

## Module 1: Introduction to CRUD Applications

### Workshop Overview

In this workshop, we'll build a complete CRUD application for managing blog posts and categories:

- Set up a Next.js project with the necessary components
- Connect to a REST API (https://ait-training-rest-api.glitch.me/)
- Implement all four CRUD operations for both blog posts and categories
- Create a user-friendly interface with Tailwind CSS and daisyUI
- Handle loading and error states

---

## Module 2: Project Setup (10 minutes)

### Creating a New Next.js Project

Let's start by Dowload a new CRUD Next.js project from <br>

LINK: https://nextjs-basic-slidev.vercel.app/workshop-crud.zip

** Please make sure you already install node version 20+ 

To insatll node_modules try to run
```bash
npm i
```

Start development 
```bash
npm run dev
```

Open [localhost:3000 ](http://localhost:3000)

<!-- Configuration options:
```
✔ Would you like to use TypeScript? … No
✔ Would you like to use ESLint? … Yes
✔ Would you like to use Tailwind CSS? … Yes
✔ Would you like to use `src/` directory? … No
✔ Would you like to use App Router? (recommended) … Yes
✔ Would you like to customize the default import alias? … No
``` -->

---

## Module 2: Project Setup (10 minutes)

### Project Structure

Our project will have the following structure:

``` {*}{maxHeight:'70%'}
nextjs-crud-app/
├── app/
│   ├── page.jsx               # Home page with welcome message
│   ├── layout.jsx             # Root layout
│   ├── blog-posts/            # Blog posts routes
│   │   ├── page.jsx           # List all blog posts
│   │   ├── new/               # Create new blog post
│   │   │   └── page.jsx
│   │   ├── [id]/              # Dynamic route for single blog post
│   │   │   ├── page.jsx       # View blog post details
│   │   │   └── edit/          # Edit blog post
│   │   │       └── page.jsx
│   ├── categories/            # Categories routes
│   │   ├── page.jsx           # List all categories
│   │   ├── new/               # Create new category
│   │   │   └── page.jsx
│   │   ├── [id]/              # Dynamic route for single category
│   │   │   ├── page.jsx       # View category details
│   │   │   └── edit/          # Edit category
│   │   │       └── page.jsx
│   ├── services/              # API service functions
│   │   ├── blogPostService.js # Blog posts API functions
│   │   └── categoryService.js # Categories API functions
│   └── components/            # Shared components
│       ├── Hero.jsx           # Welcome hero section
│       ├── ApiEndpoints.jsx   # Display API endpoints
│       ├── BlogPostCard.jsx   # Blog post card component
│       ├── BlogPostForm.jsx   # Form for creating/editing blog posts
│       ├── CategoryCard.jsx   # Category card component
│       ├── CategoryForm.jsx   # Form for creating/editing categories
│       ├── LoadingSpinner.jsx # Loading indicator
│       └── ErrorAlert.jsx     # Error message display
├── public/
└── package.json
```

---
layout: two-cols-header
---

## Module 3: Setting Up the API Connection (5 minutes)

### Understanding the API

We'll use the REST API at https://ait-training-rest-api.glitch.me/ which provides endpoints for both blog posts and categories:

::left::

#### Blog Posts Endpoints:
- GET `/blog_posts` - List all blog posts
- GET `/blog_posts/:id` - Get a single blog post
- POST `/blog_posts` - Create a new blog post
- PUT `/blog_posts/:id` - Update a blog post
- DELETE `/blog_posts/:id` - Delete a blog post

::right::

#### Each blog post has the following structure:
```json
{
  "id": 1,
  "title": "Blog post title",
  "content": "Blog post content",
  "category": {
    "id": 1,
    "title": "Category name"
  }
}
```

---
layout: two-cols-header
---

## Module 3: Setting Up the API Connection

### Understanding the API

We'll use the REST API at https://ait-training-rest-api.glitch.me/ which provides endpoints for both blog posts and categories:

::left::

#### Categories Endpoints:
- GET `/categories` - List all categories
- GET `/categories/:id` - Get a single category
- POST `/categories` - Create a new category
- PUT `/categories/:id` - Update a category
- DELETE `/categories/:id` - Delete a category

::right::

#### Each category has the following structure:
```json
{
  "id": 1,
  "title": "Category name"
}
```

---
hide: true
---

## Module 3: Setting Up the API Connection

### What is an API Service?

- API services are helper functions that handle communication with our backend
- They keep API-related code organized and reusable
- Make it easier to change the API URL or add features like authentication later

---
hide: true
---
## Module 3: Setting Up the API Connection

### Installing Axios

First, we need to install axios, a popular library for making HTTP requests:

```bash
npm install axios
```

Why Axios?
- Easy to use
- Works in all browsers
- Handles responses and errors nicely
- Supports modern JavaScript features

---

## Module 3: Setting Up the API Connection

### Blog Post Service Setup

Let's create our first service file:

```jsx
// app/services/blogPostService.js
import axios from 'axios';

// Store the API URL in a constant so it's easy to change later
const API_URL = 'https://ait-training-rest-api.glitch.me/blog_posts';
```

This sets up:
- The import for axios
- A constant for our API URL
- The foundation for our service functions

---
layout: two-cols-header
---

## Module 3: Setting Up the API Connection (10 minutes)

### Getting All Blog Posts

Our first API function gets the list of all blog posts:

::left::

```jsx
// app/services/blogPostService.js
// ...existing code...

export const getBlogPosts = async () => {
  try {
    // Send GET request to the API
    const response = await axios.get(API_URL);
    // Return just the data part of the response
    return response.data;
  } catch (error) {
    // If something goes wrong, log it and re-throw
    console.error('Error fetching blog posts:', error);
    throw error;
  }
};
```

::right::

What this does:
1. Makes a GET request to our API
2. Returns the list of blog posts if successful
3. Handles any errors that might occur

---
layout: two-cols-header
---


## Module 3: Setting Up the API Connection

### Getting a Single Blog Post

::left::

Function to fetch one specific blog post:

```jsx
// app/services/blogPostService.js
// ...existing code...

export const getBlogPostByID = async (id) => {
  try {
    // Send GET request with the post ID in the URL
    const response = await axios.get(`${API_URL}/${id}`);
    return response.data;
  } catch (error) {
    console.error(`Error fetching blog post with id ${id}:`, error);
    throw error;
  }
};
```

::right::

What this does:
1. Takes a blog post ID as parameter
2. Adds the ID to the API URL
3. Returns the specific blog post

---
layout: two-cols-header
---


## Module 3: Setting Up the API Connection

### Creating a New Blog Post

::left::

Function to create a new blog post:

```jsx
// app/services/blogPostService.js
// ...existing code...

export const createBlogPost = async (blogPost) => {
  try {
    // Send POST request with the blog post data
    const response = await axios.post(API_URL, blogPost);
    return response.data;
  } catch (error) {
    console.error('Error creating blog post:', error);
    throw error;
  }
};
```

::right::

What this does:
1. Takes new blog post data as parameter
2. Sends a POST request with the data
3. Returns the created blog post from the server

---
layout: two-cols-header
---

## Module 3: Setting Up the API Connection

### Updating and Deleting Blog Posts

::left::

Functions for modifying existing posts:

```jsx {*}{maxHeight:'70%'}
// app/services/blogPostService.js
// ...existing code...

// Update an existing blog post
export const updateBlogPost = async (id, blogPost) => {
  try {
    // Send PUT request with updated data
    const response = await axios.put(`${API_URL}/${id}`, blogPost);
    return response.data;
  } catch (error) {
    console.error(`Error updating blog post with id ${id}:`, error);
    throw error;
  }
};

// Delete a blog post
export const deleteBlogPost = async (id) => {
  try {
    // Send DELETE request
    await axios.delete(`${API_URL}/${id}`);
    return true;
  } catch (error) {
    console.error(`Error deleting blog post with id ${id}:`, error);
    throw error;
  }
};
```

::right::

Key Points:
1. Update function needs both ID and new data
2. Delete function only needs the ID
3. Both handle errors similarly to other functions

---

## Module 3: Setting Up the API Connection

### Workshop: Create Your Own Category Service

Now it's your turn!  
**Create `app/services/categoryService.js`** with similar functions for categories:

- Use API URL: `https://ait-training-rest-api.glitch.me/categories`
- Implement:
  - `getCategories()`
  - `getCategory(id)`
  - `createCategory(category)`
  - `updateCategory(id, category)`
  - `deleteCategory(id)`

**Tip:**  
Follow the same structure as `blogPostService.js`.  
Handle errors in the same way.

---

## Module 3: Setting Up the API Connection (15 mins)

### Solution: Category Service

If you get stuck, here's the solution:

```jsx {*}{maxHeight:'70%'}
// app/services/categoryService.js
import axios from 'axios';

const API_URL = 'https://ait-training-rest-api.glitch.me/categories';

export const getCategories = async () => {
  try {
    const response = await axios.get(API_URL);
    return response.data;
  } catch (error) {
    console.error('Error fetching categories:', error);
    throw error;
  }
};

export const getCategory = async (id) => {
  try {
    const response = await axios.get(`${API_URL}/${id}`);
    return response.data;
  } catch (error) {
    console.error(`Error fetching category with id ${id}:`, error);
    throw error;
  }
};

export const createCategory = async (category) => {
  try {
    const response = await axios.post(API_URL, category);
    return response.data;
  } catch (error) {
    console.error('Error creating category:', error);
    throw error;
  }
};

export const updateCategory = async (id, category) => {
  try {
    const response = await axios.put(`${API_URL}/${id}`, category);
    return response.data;
  } catch (error) {
    console.error(`Error updating category with id ${id}:`, error);
    throw error;
  }
};

export const deleteCategory = async (id) => {
  try {
    await axios.delete(`${API_URL}/${id}`);
    return true;
  } catch (error) {
    console.error(`Error deleting category with id ${id}:`, error);
    throw error;
  }
};
```

---

## Module 4: Creating the Home Page (5 minutes)

### Implementing the Hero Component

First, let's create a hero component to welcome users to our application:

```jsx {*}{maxHeight:'70%'}
// app/components/Hero.js
import Link from "next/link";

export default function Hero() {
  return (
    <div className="hero min-h-[80vh]">
      <div className="hero-content text-center">
        <div className="max-w-md">
          <h1 className="text-5xl font-bold">Next.js CRUD Workshop</h1>
          <p className="py-6">
            Welcome to the Next.js CRUD Workshop! This application demonstrates how to build a simple CRUD (Create, Read, Update, Delete) interface for blog posts using Next.js, Tailwind CSS, and daisyUI.
          </p>
          <div className="flex flex-col md:flex-row gap-4 justify-center">
            <Link href="/blog-posts" className="btn btn-primary">
              View Blog Posts
            </Link>
            <Link href="/blog-posts/new" className="btn btn-secondary">
              Create New Post
            </Link>
          </div>
        </div>
      </div>
    </div>
  );
}
```

---
hide: true
---

### Implementing the API Endpoints Component

Next, let's create a component to display the available API endpoints:

```jsx
// app/components/ApiEndpoints.jsx
export default function ApiEndpoints() {
  return (
    <>
      <div className="divider my-8">API Endpoints</div>
      <div className="card bg-base-200 shadow-xl">
        <div className="card-body">
          <h2 className="card-title">Available Endpoints</h2>
          <ul className="list-disc list-inside text-left">
            <li>
              <span className="font-mono bg-base-300 px-2 py-1 rounded">
                https://ait-training-rest-api.glitch.me/blog_posts
              </span>
              <p className="mt-1">Example endpoint for blog posts CRUD operations</p>
            </li>
            <li className="mt-4">
              <span className="font-mono bg-base-300 px-2 py-1 rounded">
                https://ait-training-rest-api.glitch.me/categories
              </span>
              <p className="mt-1">Endpoint for categories to manage blog post categories</p>
            </li>
          </ul>
        </div>
      </div>
    </>
  );
}
```

### Implementing the Home Page

Now, let's create the home page that uses these components:

```jsx
// app/page.js
import Hero from "./components/Hero";
import ApiEndpoints from "./components/ApiEndpoints";

export default function Home() {
  return (
    <div>
      <Hero />
      <div className="max-w-md mx-auto">
        <ApiEndpoints />
      </div>
    </div>
  );
}
```

---

## Module 5: Implementing the Blog Posts List Page (Read Operation) (5 minutes)

### Creating the BlogPostCard Component

Let's create a component to display each blog post in a card:

```jsx {*}{maxHeight:'60%'}
// app/components/BlogPostCard.jsx
import Link from "next/link";

export default function BlogPostCard({ post, onDelete }) {
  return (
    <div className="card bg-base-100 shadow-xl">
      <div className="card-body">
        <h2 className="card-title">{post.title}</h2>
        <p className="line-clamp-3">{post.content}</p>

        {post.category && (
          <div className="badge badge-secondary">{post.category.title}</div>
        )}

        <div className="card-actions justify-end mt-4">
          <Link href={`/blog-posts/${post.id}`} className="btn btn-sm btn-primary">
            View
          </Link>
          <Link href={`/blog-posts/${post.id}/edit`} className="btn btn-sm btn-secondary">
            Edit
          </Link>
          <button 
            onClick={() => onDelete(post.id)} 
            className="btn btn-sm btn-error"
          >
            Delete
          </button>
        </div>
      </div>
    </div>
  );
}
```

---

## Module 5: Implementing the Blog Posts List Page (Read Operation) (10 minutes)

### Implementing the Blog Posts List Page

Now, let's create the blog posts list page that fetches and displays the blog posts:

```jsx {*}{maxHeight:'60%'}
// app/blog-posts/page.jsx
"use client";

import { useState, useEffect } from "react";
import Link from "next/link";
import { getBlogPosts, deleteBlogPost } from "../services/blogPostService";
import LoadingSpinner from "../components/LoadingSpinner";
import ErrorAlert from "../components/ErrorAlert";
import BlogPostCard from "../components/BlogPostCard";

export default function BlogPostsPage() {
  const [blogPosts, setBlogPosts] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  const fetchBlogPosts = async () => {
    try {
      setLoading(true);
      const data = await getBlogPosts();
      setBlogPosts(data);
      setError(null);
    } catch (err) {
      setError("Failed to fetch blog posts. Please try again later.");
      console.error(err);
    } finally {
      setLoading(false);
    }
  };

  useEffect(() => {
    fetchBlogPosts();
  }, []);

  const handleDelete = async (id) => {
    if (window.confirm("Are you sure you want to delete this blog post?")) {
      try {
        await deleteBlogPost(id);
        // Refresh the list after deletion
        fetchBlogPosts();
      } catch (err) {
        setError("Failed to delete blog post. Please try again later.");
        console.error(err);
      }
    }
  };

  if (loading) {
    return <LoadingSpinner />;
  }

  if (error) {
    return <ErrorAlert message={error} />;
  }

  return (
    <div>
      <div className="flex justify-between items-center mb-6">
        <h1 className="text-3xl font-bold">Blog Posts</h1>
        <Link href="/blog-posts/new" className="btn btn-primary">
          Create New Post
        </Link>
      </div>

      {blogPosts.length === 0 ? (
        <div className="alert alert-info">
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" className="stroke-current shrink-0 w-6 h-6"><path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>
          <span>No blog posts found. Create your first post!</span>
        </div>
      ) : (
        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
          {blogPosts.map((post) => (
            <BlogPostCard key={post.id} post={post} onDelete={handleDelete} />
          ))}
        </div>
      )}
    </div>
  );
}
```

---

### Step 1: Imports and Setup

```jsx
// app/blog-posts/page.jsx
"use client";

import { useState, useEffect } from "react"; // React hooks for state and lifecycle
import Link from "next/link"; // For navigation
import { getBlogPosts, deleteBlogPost } from "../services/blogPostService"; // API functions
import LoadingSpinner from "../components/LoadingSpinner"; // Loading indicator
import ErrorAlert from "../components/ErrorAlert"; // Error display
import BlogPostCard from "../components/BlogPostCard"; // Card for each blog post
```

---

### Step 2: State Variables

```jsx
// ...existing code...
export default function BlogPostsPage() {
  const [blogPosts, setBlogPosts] = useState([]); // List of blog posts
  const [loading, setLoading] = useState(true);   // Loading state
  const [error, setError] = useState(null);       // Error message
// ...existing code...
```

---

### Step 3: Fetching Blog Posts

```jsx
// ...existing code...
  const fetchBlogPosts = async () => {
    try {
      setLoading(true); // Show loading spinner
      const data = await getBlogPosts(); // Fetch posts from API
      setBlogPosts(data); // Save posts to state
      setError(null);     // Clear any previous error
    } catch (err) {
      setError("Failed to fetch blog posts. Please try again later."); // Show error
      console.error(err);
    } finally {
      setLoading(false); // Hide loading spinner
    }
  };

  useEffect(() => {
    fetchBlogPosts(); // Run once when page loads
  }, []);
```

---

### Step 4: Deleting a Blog Post

```jsx
// ...existing code...
  const handleDelete = async (id) => {
    if (window.confirm("Are you sure you want to delete this blog post?")) { // Confirm delete
      try {
        await deleteBlogPost(id); // Call API to delete
        fetchBlogPosts(); // Refresh list after deletion
      } catch (err) {
        setError("Failed to delete blog post. Please try again later."); // Show error
        console.error(err);
      }
    }
  };
// ...existing code...
```

---

### Step 5: Loading and Error States

```jsx
// ...existing code...
  if (loading) {
    return <LoadingSpinner />; // Show spinner while loading
  }

  if (error) {
    return <ErrorAlert message={error} />; // Show error if any
  }
```

---

### Step 6: Rendering the Blog Posts List

```jsx
// ...existing code...
  return (
    <div>
      <div className="flex justify-between items-center mb-6">
        <h1 className="text-3xl font-bold">Blog Posts</h1>
        <Link href="/blog-posts/new" className="btn btn-primary">
          Create New Post
        </Link>
      </div>

      {blogPosts.length === 0 ? (
        <div className="alert alert-info">
          {/* Info icon */}
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" className="stroke-current shrink-0 w-6 h-6"><path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>
          <span>No blog posts found. Create your first post!</span>
        </div>
      ) : (
        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
          {blogPosts.map((post) => (
            <BlogPostCard key={post.id} post={post} onDelete={handleDelete} /> // Show each post
          ))}
        </div>
      )}
    </div>
  );
}
// ...existing code...
```

---

### Summary

- **Imports**: Bring in React, API, and UI helpers.
- **State**: Track blog posts, loading, and errors.
- **Fetching**: Load posts from the API when the page loads.
- **Deleting**: Remove a post and refresh the list.
- **Loading/Error**: Show spinner or error message as needed.
- **Rendering**: Display posts in a grid, or an info message if none exist.

---

## Module 6: Creating the Blog Post Form Component

### Building a Reusable Form Component

Let's create a reusable form component for both creating and editing blog posts:

```jsx {*}{maxHeight:'60%'}
// app/components/BlogPostForm.js
"use client";

import { useState, useEffect } from "react";
import Link from "next/link";
import ErrorAlert from "./ErrorAlert";
import { getCategories } from "../services/categoryService";

export default function BlogPostForm({ initialData = { title: "", content: "", category: { id: "" } }, onSubmit, isLoading }) {
  const [formData, setFormData] = useState(initialData);
  const [categories, setCategories] = useState([]);
  const [error, setError] = useState(null);
  const [loadingCategories, setLoadingCategories] = useState(true);

  useEffect(() => {
    const fetchCategories = async () => {
      try {
        setLoadingCategories(true);
        const data = await getCategories();
        setCategories(data);
      } catch (err) {
        console.error("Error fetching categories:", err);
      } finally {
        setLoadingCategories(false);
      }
    };

    fetchCategories();
  }, []);

  const handleChange = (e) => {
    const { name, value } = e.target;

    if (name === "categoryId") {
      setFormData(prev => ({
        ...prev,
        category: { id: parseInt(value) }
      }));
    } else {
      setFormData(prev => ({
        ...prev,
        [name]: value
      }));
    }
  };

  const handleSubmit = async (e) => {
    e.preventDefault();

    // Basic validation
    if (!formData.title.trim() || !formData.content.trim()) {
      setError("Title and content are required");
      return;
    }

    setError(null);
    onSubmit(formData);
  };

  return (
    <div>
      {error && <ErrorAlert message={error} />}

      <div className="card bg-base-100 shadow-xl">
        <div className="card-body">
          <form onSubmit={handleSubmit}>
            <div className="form-control w-full">
              <label className="label">
                <span className="label-text">Title</span>
              </label>
              <input
                type="text"
                name="title"
                value={formData.title}
                onChange={handleChange}
                placeholder="Enter blog post title"
                className="input input-bordered w-full"
                disabled={isLoading}
              />
            </div>

            <div className="form-control w-full mt-4">
              <label className="label">
                <span className="label-text">Content</span>
              </label>
              <textarea
                name="content"
                value={formData.content}
                onChange={handleChange}
                placeholder="Enter blog post content"
                className="textarea textarea-bordered w-full h-64"
                disabled={isLoading}
              ></textarea>
            </div>

            <div className="form-control w-full mt-4">
              <label className="label">
                <span className="label-text">Category</span>
              </label>
              <select
                name="categoryId"
                value={formData.category?.id || ""}
                onChange={handleChange}
                className="select select-bordered w-full"
                disabled={isLoading || loadingCategories}
              >
                <option value="" disabled>Select a category</option>
                {categories.map(category => (
                  <option key={category.id} value={category.id}>
                    {category.title}
                  </option>
                ))}
              </select>
              {loadingCategories && (
                <div className="mt-2 text-sm text-gray-500">
                  <span className="loading loading-spinner loading-xs"></span>
                  <span className="ml-2">Loading categories...</span>
                </div>
              )}
            </div>

            <div className="card-actions justify-end mt-6">
              <Link href="/blog-posts" className="btn btn-ghost">
                Cancel
              </Link>
              <button 
                type="submit" 
                className="btn btn-primary"
                disabled={isLoading}
              >
                {isLoading ? (
                  <>
                    <span className="loading loading-spinner loading-sm"></span>
                    Saving...
                  </>
                ) : "Save Post"}
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>
  );
}
```

---

## Module 7: Implementing Create Operation

### Creating the "New Blog Post" Page

Let's implement the page for creating new blog posts:

```jsx {*}{maxHeight:'60%'}
// app/blog-posts/new/page.js
"use client";

import { useState } from "react";
import { useRouter } from "next/navigation";
import Link from "next/link";
import { createBlogPost } from "../../services/blogPostService";
import BlogPostForm from "../../components/BlogPostForm";

export default function NewBlogPostPage() {
  const router = useRouter();
  const [loading, setLoading] = useState(false);

  const handleSubmit = async (formData) => {
    try {
      setLoading(true);
      await createBlogPost(formData);
      router.push("/blog-posts");
    } catch (err) {
      console.error(err);
      throw new Error("Failed to create blog post. Please try again later.");
    } finally {
      setLoading(false);
    }
  };

  return (
    <div>
      <div className="flex justify-between items-center mb-6">
        <h1 className="text-3xl font-bold">Create New Blog Post</h1>
        <Link href="/blog-posts" className="btn btn-ghost">
          Cancel
        </Link>
      </div>

      <BlogPostForm onSubmit={handleSubmit} isLoading={loading} />
    </div>
  );
}
```

---

## Module 8: Implementing Read Single Item Operation

### Creating the Blog Post Detail Page

Let's create a page to view a single blog post's details:

```jsx {*}{maxHeight:'60%'}
// app/blog-posts/[id]/page.js
"use client";

import { useState, useEffect } from "react";
import Link from "next/link";
import { useRouter } from "next/navigation";
import { getBlogPostById, deleteBlogPost } from "../../services/blogPostService";
import LoadingSpinner from "../../components/LoadingSpinner";
import ErrorAlert from "../../components/ErrorAlert";

export default function BlogPostDetailPage({ params }) {
  const router = useRouter();
  const { id } = React.use(params);

  const [blogPost, setBlogPost] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);
  const [isDeleting, setIsDeleting] = useState(false);

  useEffect(() => {
    const fetchBlogPost = async () => {
      try {
        setLoading(true);
        const data = await getBlogPostById(id);
        setBlogPost(data);
        setError(null);
      } catch (err) {
        setError("Failed to fetch blog post. Please try again later.");
        console.error(err);
      } finally {
        setLoading(false);
      }
    };

    fetchBlogPost();
  }, [id]);

  const handleDelete = async () => {
    if (window.confirm("Are you sure you want to delete this blog post?")) {
      try {
        setIsDeleting(true);
        await deleteBlogPost(id);
        router.push("/blog-posts");
      } catch (err) {
        setError("Failed to delete blog post. Please try again later.");
        console.error(err);
      } finally {
        setIsDeleting(false);
      }
    }
  };

  if (loading) {
    return <LoadingSpinner />;
  }

  if (error) {
    return <ErrorAlert message={error} />;
  }

  return (
    <div>
      <div className="mb-6">
        <Link href="/blog-posts" className="btn btn-ghost">
          ← Back to Blog Posts
        </Link>
      </div>

      <div className="card bg-base-100 shadow-xl">
        <div className="card-body">
          <h1 className="card-title text-3xl">{blogPost.title}</h1>

          {blogPost.category && (
            <div className="badge badge-secondary">{blogPost.category.title}</div>
          )}

          <div className="divider"></div>

          <div className="whitespace-pre-line">{blogPost.content}</div>

          <div className="card-actions justify-end mt-6">
            <Link href={`/blog-posts/${id}/edit`} className="btn btn-primary">
              Edit
            </Link>
            <button 
              onClick={handleDelete} 
              className="btn btn-error"
              disabled={isDeleting}
            >
              {isDeleting ? (
                <>
                  <span className="loading loading-spinner loading-sm"></span>
                  Deleting...
                </>
              ) : "Delete"}
            </button>
          </div>
        </div>
      </div>
    </div>
  );
}
```

---

## Module 9: Implementing Update Operation

### Creating the Edit Blog Post Page

Let's implement the page for editing existing blog posts:

```jsx {*}{maxHeight:'60%'}
// app/blog-posts/[id]/edit/page.js
"use client";

import React, { useState, useEffect } from "react";
import { useRouter } from "next/navigation";
import Link from "next/link";
import { getBlogPost, updateBlogPost } from "../../../services/blogPostService";
import BlogPostForm from "../../../components/BlogPostForm";

export default function EditBlogPostPage({ params }) {
  const router = useRouter();
  const { id } = React.use(params);

  const [blogPost, setBlogPost] = useState(null);
  const [loading, setLoading] = useState(true);
  const [submitting, setSubmitting] = useState(false);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchBlogPost = async () => {
      try {
        setLoading(true);
        const data = await getBlogPost(id);
        setBlogPost(data);
        setError(null);
      } catch (err) {
        setError("Failed to fetch blog post. Please try again later.");
        console.error(err);
      } finally {
        setLoading(false);
      }
    };

    fetchBlogPost();
  }, [id]);

  const handleSubmit = async (formData) => {
    try {
      setSubmitting(true);
      await updateBlogPost(id, formData);
      router.push(`/blog-posts/${id}`);
    } catch (err) {
      setError("Failed to update blog post. Please try again later.");
      console.error(err);
    } finally {
      setSubmitting(false);
    }
  };

  if (loading) {
    return (
      <div className="flex justify-center items-center min-h-[60vh]">
        <span className="loading loading-spinner loading-lg text-primary"></span>
      </div>
    );
  }

  if (error) {
    return (
      <div className="alert alert-error">
        <svg xmlns="http://www.w3.org/2000/svg" className="stroke-current shrink-0 h-6 w-6" fill="none" viewBox="0 0 24 24"><path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z" /></svg>
        <span>{error}</span>
      </div>
    );
  }

  return (
    <div>
      <div className="flex justify-between items-center mb-6">
        <h1 className="text-3xl font-bold">Edit Blog Post</h1>
        <Link href={`/blog-posts/${id}`} className="btn btn-ghost">
          Cancel
        </Link>
      </div>

      <BlogPostForm 
        initialData={blogPost} 
        onSubmit={handleSubmit} 
        isLoading={submitting} 
      />
    </div>
  );
}
```
---

## Module 10: Implementing Categories CRUD (5 minutes)

### Creating the Category Card Component

Let's create a component to display each category in a card:

```jsx {*}{maxHeight:'60%'}
// app/components/CategoryCard.js
import Link from "next/link";

export default function CategoryCard({ category, onDelete }) {
  return (
    <div className="card bg-base-100 shadow-xl">
      <div className="card-body">
        <h2 className="card-title">{category.title}</h2>
        <div className="card-actions justify-end mt-4">
          <Link href={`/categories/${category.id}`} className="btn btn-sm btn-outline">
            View
          </Link>
          <Link href={`/categories/${category.id}/edit`} className="btn btn-sm btn-outline btn-accent">
            Edit
          </Link>
          <button 
            onClick={() => onDelete(category.id)} 
            className="btn btn-sm btn-outline btn-error"
          >
            Delete
          </button>
        </div>
      </div>
    </div>
  );
}
```

---

### Creating the Category Form Component (5 minutes)

Let's create a reusable form component for both creating and editing categories:

```jsx {*}{maxHeight:'60%'}
// app/components/CategoryForm.js
"use client";

import { useState } from "react";
import Link from "next/link";
import ErrorAlert from "./ErrorAlert";

export default function CategoryForm({ initialData = { title: "" }, onSubmit, isLoading }) {
  const [formData, setFormData] = useState(initialData);
  const [error, setError] = useState(null);

  const handleChange = (e) => {
    const { name, value } = e.target;
    setFormData(prev => ({
      ...prev,
      [name]: value
    }));
  };

  const handleSubmit = async (e) => {
    e.preventDefault();

    // Basic validation
    if (!formData.title.trim()) {
      setError("Title is required");
      return;
    }

    setError(null);
    onSubmit(formData);
  };

  return (
    <div>
      {error && <ErrorAlert message={error} />}

      <div className="card bg-base-100 shadow-xl">
        <div className="card-body">
          <form onSubmit={handleSubmit}>
            <div className="form-control w-full">
              <label className="label">
                <span className="label-text">Title</span>
              </label>
              <input
                type="text"
                name="title"
                value={formData.title}
                onChange={handleChange}
                placeholder="Enter category title"
                className="input input-bordered w-full"
                disabled={isLoading}
              />
            </div>

            <div className="card-actions justify-end mt-6">
              <Link href="/categories" className="btn btn-ghost">
                Cancel
              </Link>
              <button 
                type="submit" 
                className="btn btn-primary"
                disabled={isLoading}
              >
                {isLoading ? (
                  <>
                    <span className="loading loading-spinner loading-sm"></span>
                    Saving...
                  </>
                ) : "Save Category"}
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>
  );
}
```

---

### Implementing the Categories List Page (10 minutes)

Now, let's create the categories list page:

```jsx {*}{maxHeight:'60%'}
// app/categories/page.jsx
"use client";

import { useState, useEffect } from "react";
import Link from "next/link";
import { getCategories, deleteCategory } from "../services/categoryService";
import LoadingSpinner from "../components/LoadingSpinner";
import ErrorAlert from "../components/ErrorAlert";
import CategoryCard from "../components/CategoryCard";

export default function CategoriesPage() {
  const [categories, setCategories] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  const fetchCategories = async () => {
    try {
      setLoading(true);
      const data = await getCategories();
      setCategories(data);
      setError(null);
    } catch (err) {
      setError("Failed to fetch categories. Please try again later.");
      console.error(err);
    } finally {
      setLoading(false);
    }
  };

  useEffect(() => {
    fetchCategories();
  }, []);

  const handleDelete = async (id) => {
    if (window.confirm("Are you sure you want to delete this category?")) {
      try {
        await deleteCategory(id);
        // Refresh the list after deletion
        fetchCategories();
      } catch (err) {
        setError("Failed to delete category. Please try again later.");
        console.error(err);
      }
    }
  };

  if (loading) {
    return <LoadingSpinner />;
  }

  if (error) {
    return <ErrorAlert message={error} />;
  }

  return (
    <div>
      <div className="flex justify-between items-center mb-6">
        <h1 className="text-3xl font-bold">Categories</h1>
        <Link href="/categories/new" className="btn btn-primary">
          Create New Category
        </Link>
      </div>

      {categories.length === 0 ? (
        <div className="alert alert-info">
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" className="stroke-current shrink-0 w-6 h-6"><path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>
          <span>No categories found. Create your first category!</span>
        </div>
      ) : (
        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
          {categories.map((category) => (
            <CategoryCard key={category.id} category={category} onDelete={handleDelete} />
          ))}
        </div>
      )}
    </div>
  );
}
```

---

## Module 10: Error Handling and Loading States

### Implementing Error Handling

Let's create error and loading UI components:

```jsx {*}{maxHeight:'60%'}
// app/components/ErrorMessage.jsx
export default function ErrorMessage({ message }) {
  return (
    <div className="bg-red-100 border border-red-400 text-red-700 px-4 py-3 rounded mb-4">
      {message}
    </div>
  );
}

// app/components/LoadingSpinner.jsx
export default function LoadingSpinner() {
  return (
    <div className="flex justify-center items-center p-8">
      <div className="animate-spin rounded-full h-12 w-12 border-t-2 border-b-2 border-blue-500"></div>
    </div>
  );
}
```

---
hide: true
---

## Module 10: Error Handling and Loading States (15 minutes)

### Adding Error Boundaries

Let's create an error boundary for our app:

```jsx {*}{maxHeight:'60%'}
// app/error.jsx
'use client';

import { useEffect } from 'react';
import Link from 'next/link';

export default function Error({ error }) {
  useEffect(() => {
    // Log the error to an error reporting service
    console.error(error);
  }, [error]);

  return (
    <div className="container mx-auto p-8 text-center">
      <h2 className="text-2xl font-bold mb-4">Something went wrong!</h2>
      <p className="mb-4 text-red-600">{error.message || 'An unexpected error occurred'}</p>
      <div className="flex justify-center space-x-4">
        <Link
          href="/"
          className="bg-gray-500 text-white px-4 py-2 rounded hover:bg-gray-600"
        >
          Go back home
        </Link>
      </div>
    </div>
  );
}
```

---

## Workshop Summary

In this workshop, we've built a complete CRUD application with Next.js:

1. **Created a Next.js project** with the App Router
2. **Connected to a REST API** for data operations using axios
3. **Implemented all CRUD operations for blog posts and categories**:
   - Create: Adding new blog posts and categories
   - Read: Displaying lists and details of blog posts and categories
   - Update: Editing existing blog posts and categories
   - Delete: Removing blog posts and categories
4. **Added error handling and loading states**
5. **Created a responsive UI** with Tailwind CSS and daisyUI
6. **Implemented relationships** between blog posts and categories

---
hide: true
---

This foundation can be extended with:
- Authentication and authorization
- More complex data relationships
- Advanced form validation with libraries like Zod or Yup
- Optimistic UI updates for better user experience
- Server-side mutations with Server Actions
- Image uploads for blog posts
- Rich text editing for blog post content

