# 🍪 Web Cookies Overview

This README provides a detailed explanation of **cookies** in web development—how they work, their use cases, and how they compare to other client-side storage options like `localStorage` and `sessionStorage`.

---

## ✅ What Are Cookies?

**Cookies** are small pieces of data stored in the browser by the server or JavaScript. They're used to maintain **stateful information** across page requests, which HTTP does not support natively.

---

## 🔑 Key Features

- Stored as name-value pairs.
- Automatically sent to the server with **every HTTP request** to the same origin.
- Can have **expiration dates**.
- **Size limit**: ~4KB per cookie.
- Can be flagged as **HTTP-only** (inaccessible to JavaScript) or **Secure** (only over HTTPS).

---

## 🍭 Cookie Examples

### 1. Set with JavaScript
```javascript
document.cookie = "username=Alice; expires=Fri, 31 Dec 2025 23:59:59 GMT; path=/";
```

### 2. Read with JavaScript
```javascript
console.log(document.cookie);
// Output: "username=Alice"
```

### 3. Set with HTTP Header (Server-side)
```
Set-Cookie: sessionId=abc123; HttpOnly; Secure; SameSite=Strict
```

---

## ⚙️ Cookie Options

| Option       | Description |
|--------------|-------------|
| `expires`    | Sets the expiration date (UTC format). |
| `max-age`    | Number of seconds until expiration. |
| `path`       | Limits the cookie to a specific path. |
| `domain`     | Specifies the domain for which the cookie is valid. |
| `Secure`     | Sends cookie only over HTTPS. |
| `HttpOnly`   | Prevents JavaScript access to the cookie. |
| `SameSite`   | Controls cross-site cookie behavior (`Strict`, `Lax`, `None`). |

---

## 🧠 When to Use Cookies

- **Authentication tokens** (e.g. session IDs).
- **Tracking user activity** (e.g. analytics, preferences).
- When data needs to be **sent to the server** on every request.
- For compatibility with **older browsers**.

---

## 🔍 Cookies vs Web Storage

| Feature          | Cookies                        | localStorage / sessionStorage   |
|------------------|--------------------------------|----------------------------------|
| Sent with HTTP   | ✅ Automatically               | ❌ Not sent with requests        |
| Max Size         | ~4KB per cookie                | ~5–10MB                         |
| Expiration       | Can be set                     | sessionStorage = on tab close; localStorage = manual |
| Accessible via JS| ✅ (unless `HttpOnly`)         | ✅                               |
| Secure Options   | ✅ (`Secure`, `HttpOnly`)      | ❌                               |
| Primary Use      | Server communication, auth     | Client-side persistence          |

---

## ⚠️ Caution

- Avoid storing sensitive info unless using `Secure` and `HttpOnly`.
- Overuse can degrade performance due to cookie size inflating HTTP requests.
