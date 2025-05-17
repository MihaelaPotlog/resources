

# 🗃️ Web Storage Overview

This README provides a clear comparison between `sessionStorage`, `localStorage`, and `IndexedDB`, the main client-side storage options available in modern web browsers.

---

## 🔒 Session Storage

### Description
- Stores data for the **duration of the page session**.
- Data is **cleared when the tab is closed**.

### Features
- **Scope**: Per-tab, per-origin.
- **Capacity**: ~5MB (varies by browser).
- **Access**: Synchronous, JavaScript-accessible.

### Use Cases
- Temporary data (e.g., form wizards).
- UI state specific to a tab.

### Example
```javascript
sessionStorage.setItem("username", "Alice");
const user = sessionStorage.getItem("username"); // "Alice"
```

---

## 💾 Local Storage

### Description
- Stores data **persistently** across browser sessions.
- Data remains until explicitly cleared.

### Features
- **Scope**: Shared across all tabs/windows of the same origin.
- **Capacity**: ~5–10MB.
- **Access**: Synchronous, JavaScript-accessible.

### Use Cases
- Theme preferences.
- Cached data that doesn’t expire.
- Lightweight user settings.

### Example
```javascript
localStorage.setItem("theme", "dark");
const theme = localStorage.getItem("theme"); // "dark"
```

---

## 🧠 IndexedDB

### Description
- A **low-level NoSQL database** built into the browser.
- Supports storing large, structured data and binary blobs.

### Features
- **Async API** (non-blocking).
- **Data Types**: Almost any JavaScript object.
- **Complex Queries**: Use indexes and cursors.
- **Capacity**: Hundreds of MBs to GBs, depending on browser.
- **Scope**: Per-origin.

### Use Cases
- Offline apps (e.g., Progressive Web Apps).
- Caching large amounts of data (e.g., images, audio).
- Storing and syncing complex structured data.

### Example (with `idb` helper)
```javascript
import { openDB } from 'idb';

const db = await openDB('MyDB', 1, {
  upgrade(db) {
    db.createObjectStore('users', { keyPath: 'id' });
  },
});

// Store data
await db.put('users', { id: 1, name: 'Alice' });

// Retrieve data
const user = await db.get('users', 1);
console.log(user.name); // "Alice"
```

---

## 🔍 Feature Comparison

| Feature            | `sessionStorage`        | `localStorage`           | `IndexedDB`              |
|--------------------|-------------------------|---------------------------|---------------------------|
| Persistence        | Until tab is closed     | Until explicitly cleared  | Persistent                |
| Scope              | Per-tab, per-origin     | Per-origin                | Per-origin                |
| Capacity           | ~5MB                    | ~5–10MB                   | 100MB+                    |
| Data Types         | Strings only            | Strings only              | Objects, files, blobs     |
| Access Type        | Synchronous             | Synchronous               | Asynchronous (Promise)    |
| Complex Queries    | ❌                      | ❌                        | ✅                        |
| Indexed Search     | ❌                      | ❌                        | ✅                        |

---

## ⚠️ Notes

- Do **not** store sensitive data (e.g., passwords) in any Web Storage.
- Use `IndexedDB` for large or complex datasets.
- Use `localStorage` or `sessionStorage` for simple key-value pairs.
