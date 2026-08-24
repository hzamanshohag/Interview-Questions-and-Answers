# React.js & Next.js Interview Questions & Answers 🚀

A comprehensive collection of **React.js and Next.js interview questions, answers, concepts, and modern development topics**.

---

## 📚 Topics Covered

### ⚛️ React.js Basics

* What is React?
* How does React work?
* React Components
* Functional vs Class Components
* JSX
* Virtual DOM
* Rendering & Re-rendering
* Reconciliation
* Keys
* React Suspense
* React Strict Mode

---

### 🔄 State & Props

* State vs Props
* Parent to Child Communication
* Prop Drilling
* Lifting State Up
* Controlled Components
* Uncontrolled Components
* Functional State Updates
* State Batching
* State Preservation & Resetting

---

### 🪝 React Hooks

* `useState`
* `useEffect`
* `useLayoutEffect`
* `useContext`
* `useReducer`
* `useRef`
* `useMemo`
* `useCallback`
* `useId`
* `useTransition`
* `useDeferredValue`
* `useImperativeHandle`
* `useActionState`
* `use`
* Custom Hooks

---

### ⚡ React Performance

* Preventing unnecessary re-renders
* `React.memo`
* `useMemo` vs `useCallback`
* React Profiler
* Code Splitting
* `React.lazy`
* Suspense
* Memory Leaks
* Request Cancellation
* Optimistic UI
* React Compiler

---

### 📝 React Forms & Data Fetching

* Controlled vs Uncontrolled Forms
* Form Validation
* Form Submission
* `FormData`
* Data Fetching with `useEffect`
* React Query / TanStack Query
* SWR
* Loading & Error States
* Pagination
* Infinite Scrolling
* Caching
* Optimistic Updates

---

### 🗂️ React State Management

* Local State
* Lifted State
* Context API
* `useReducer`
* Redux Toolkit
* Zustand
* Server State vs Client State

---

### 🧪 React Testing

* Unit Testing
* Component Testing
* Integration Testing
* React Testing Library
* Vitest / Jest
* Mocking
* Async Testing
* Playwright / Cypress

---

### ♿ Accessibility & Security

#### Accessibility

* Semantic HTML
* ARIA
* Keyboard Navigation
* Focus Management
* Accessible Forms
* Screen Reader Support

#### Security

* XSS Prevention
* `dangerouslySetInnerHTML`
* CSRF Concepts
* Secure Token Storage
* Dependency Security
* Environment Variables

---

# ▲ Next.js

## 🚀 Next.js Fundamentals

* What is Next.js?
* Why was Next.js created?
* Next.js vs Traditional React
* File-Based Routing
* API Routes
* Route Handlers
* Middleware / Proxy
* Hydration
* Hydration Mismatch

---

## 🖥️ Rendering Strategies

* Client-Side Rendering (CSR)
* Server-Side Rendering (SSR)
* Static Site Generation (SSG)
* Incremental Static Regeneration (ISR)
* Static Rendering
* Dynamic Rendering
* Streaming
* Suspense Boundaries

---

## 📁 Next.js App Router

* `app/` Directory
* `page.tsx`
* `layout.tsx`
* `loading.tsx`
* `error.tsx`
* `not-found.tsx`
* `template.tsx`
* Route Groups
* Dynamic Routes
* Catch-all Routes
* Parallel Routes
* Intercepting Routes

---

## 🖥️ Server vs Client Components

### Server Components

* Render on the server
* Access server-side resources
* Reduce client-side JavaScript
* Can access databases directly

### Client Components

Use:

```tsx
"use client";
```

Required for:

* State
* Event Handlers
* Browser APIs
* Interactive UI
* Client-side Hooks

---

## 🔥 Server Actions & Server Functions

Topics include:

* `"use server"`
* Form Actions
* Data Mutations
* Validation
* Authentication
* Authorization
* Error Handling
* `useActionState`
* `useTransition`
* Optimistic Updates
* Cache Revalidation

---

## 💾 Next.js Caching

Understand:

* Request Memoization
* Data Cache
* Full Route Cache
* Client Router Cache
* Time-Based Revalidation
* On-Demand Revalidation
* `revalidatePath`
* `revalidateTag`
* Cache Invalidation

---

## 🌐 Routing

* Static Routes
* Dynamic Segments `[id]`
* Catch-all Routes `[...slug]`
* Optional Catch-all `[[...slug]]`
* Route Groups `(group)`
* Parallel Routes `@slot`
* Intercepting Routes
* `Link`
* `useRouter`
* `usePathname`
* `useSearchParams`
* Redirects

---

## 🔌 Route Handlers

Modern Next.js API endpoints:

```text
app/api/users/route.ts
```

Supported HTTP methods:

* `GET`
* `POST`
* `PUT`
* `PATCH`
* `DELETE`

---

## ❌ Error Handling

* `error.tsx`
* `not-found.tsx`
* `notFound()`
* `redirect()`
* `loading.tsx`
* Error Boundaries
* Expected Errors
* Runtime Errors

---

## 🔍 SEO & Metadata

* Static Metadata
* `generateMetadata`
* Open Graph
* Twitter / X Metadata
* Canonical URLs
* Robots
* Sitemap
* Structured Data / JSON-LD

---

## 🔐 Authentication & Authorization

* Authentication vs Authorization
* JWT
* Cookies
* Protected Routes
* Role-Based Access Control (RBAC)
* Server-side Authorization
* Middleware / Proxy
* Secure Server Actions

---

## 🖼️ Performance Optimization

* `next/image`
* `next/font`
* Image Optimization
* Font Optimization
* Code Splitting
* Lazy Loading
* Core Web Vitals
* LCP
* CLS
* INP

---

## 🚢 Deployment

* `next build`
* `next start`
* Vercel Deployment
* Node.js Deployment
* Docker
* CDN
* Environment Variables
* Production Caching
* Logging
* Monitoring

---

# 🎯 Interview Preparation Levels

## 🟢 Tier 1 — Essential

Core concepts every React and Next.js developer should know:

* Components
* Props & State
* Hooks
* Virtual DOM
* Re-rendering
* Reconciliation
* Keys
* Context API
* Controlled Forms
* Server vs Client Components
* App Router
* Server Actions
* Caching
* Route Handlers
* Authentication
* SEO

---

## 🟡 Tier 2 — Strong Knowledge

For developers preparing for more competitive roles:

* `useTransition`
* `useDeferredValue`
* `useId`
* `useImperativeHandle`
* Code Splitting
* React Profiler
* Optimistic UI
* Request Cancellation
* Parallel Data Fetching
* Route Groups
* Parallel Routes
* Intercepting Routes
* Environment Variables
* Image & Font Optimization

---

## 🔴 Tier 3 — Advanced

Advanced concepts for experienced developers:

* React Compiler
* `use`
* `useActionState`
* Advanced Cache Invalidation
* Architecture Patterns
* Performance Profiling
* Testing Strategy
* Accessibility Strategy
* Security Architecture
* Large-Scale State Management
* Rendering Architecture & Trade-offs

---

## 🛠️ Technologies Covered

* React.js
* Next.js
* JavaScript
* TypeScript
* React Router
* Redux Toolkit
* Zustand
* TanStack Query
* SWR
* Server Components
* Server Actions
* REST APIs

---