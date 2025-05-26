---
# You can also start simply with 'default'
theme: default
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: React & Next.js 
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# open graph
# seoMeta:
#  ogImage: https://cover.sli.dev
fonts:
  sans: Geist
  mono: Geist Mono
---

## Welcome to 
# React & Next.js Training

<div @click="$slidev.nav.next" class="mt-12 py-1" hover:bg="white op-10">
  Press Space for next page <carbon:arrow-right />
</div>

---
background: https://cover.sli.dev
layout: two-cols
---

# Introduce

## Thitikon Khamluang
**Front-End Developer** 🧑‍💻


## Nutthawat Witdumrong

**Front-End Developer**  👨‍💻 

<div class="text-center m-6 text-xl">
    Advance Innovation Technology
</div> 

::right::

<img src="/assets/qr-code.png" class="mt-5 w-52 mx-auto" />


---

# Next.js Training Overview

This comprehensive training covers React and Next.js for beginners, structured into the following modules:

- 📝 **Introduction** - Internet, modern web app concepts, JavaScript essentials
- ⚛️ **React Fundamentals** - Components, props, state, JSX, Virtual DOM
<!-- - 🔄 **Programming Paradigms** - Imperative vs. declarative programming approaches -->
- 🌐 **DOM Concepts** - Understanding the Document Object Model
- 🧩 **Next.js Fundamentals** - Core features, advantages over plain React
- 🔍 **React vs. Next.js** - Key differences and when to use each framework
- 💻 **Practical Workshop** - Building a real Next.js application step-by-step

<br>

This training will take you from React basics to building full Next.js applications with modern features.

---

## Table of contents 

<Toc minDepth="1" class="mt5" maxDepth="1" columns="2" />

---
src: ./pages/0000-how-the-webs-work.md
hide: false
---

---
src: ./pages/0100-introduction.md
hide: false
---

---
src: ./pages/0200-what-is-react.md
hide: false
---

---
src: ./pages/0202-imperative-vs-declarative-programming.md
hide: false
---

---
src: ./pages/0500-what-is-dom.md
hide: false
---

---
src: ./pages/0700-virtual-dom.md
hide: false
---

---
src: ./pages/0600-what-is-jsx.md
hide: false
---

---
src: ./pages/0800-props-state-examples.md
hide: false
---

---
src: ./pages/0300-what-is-nextjs.md
hide: false
---

---
src: ./pages/0400-react-vs-nextjs.md
hide: false
---

---
src: ./pages/0900-nextjs-workshop.md
hide: false
---

---
src: ./pages/0910-nextjs-workshop-crud.md
hide: false
---


---
layout: two-cols-header
---

# References & Resources

## React & Next.js Official Documentation
- [Next.js Documentation](https://nextjs.org/docs)
- [React Server Components](https://nextjs.org/docs/app/building-your-application/rendering/server-components)
- [Data Fetching in Next.js](https://nextjs.org/docs/app/building-your-application/data-fetching)
- [Error Handling in React](https://react.dev/reference/react/Component#catching-rendering-errors-with-an-error-boundary)
- [Loading States in React](https://react.dev/reference/react/Suspense#displaying-a-fallback-while-content-is-loading)
<br>
<br>
::left::

## Further Learning
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)
- [daisyUI Documentation](https://daisyui.com/docs/install/)
- [Axios Documentation](https://axios-http.com/docs/intro)
- [REST API Design](https://restfulapi.net/)

::right::

## Additional Learning Resources
- [React Tutorial](https://react.dev/learn) - Step-by-step guide to learning React
- [Next.js Learn Course](https://nextjs.org/learn) - Interactive Next.js tutorials
- [React vs Next.js](https://nextjs.org/learn/react-foundations/what-is-react-and-nextjs) - Detailed comparison