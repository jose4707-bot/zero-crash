# 💥 [zero-crash](https://www.npmjs.com/package/zero-crash)
> 🛡️ Prevent silent crashes in Node.js apps in **one line**.

## 📊 Project Stats

![npm](https://img.shields.io/npm/v/zero-crash)
![downloads](https://img.shields.io/npm/dm/zero-crash)
![stars](https://img.shields.io/github/stars/AbhishekSuresh2/zero-crash)
![issues](https://img.shields.io/github/issues/AbhishekSuresh2/zero-crash)
![license](https://img.shields.io/npm/l/zero-crash)
![views](https://visitor-badge.laobi.icu/badge?page_id=AbhishekSuresh2.zero-crash)

**Global runtime crash protection for modern Node.js apps.**
Stop silent crashes, messy stack traces, and undefined exits.

**zero-crash** enforces **disciplined failures**, **clean shutdowns**, and **human-readable crash logs** — automatically.

Built for **2026 projects**, production-safe, and dependency-free.

---

## 🚀 Why zero-crash?

Most Node apps crash in ugly ways:

* Silent exits
* Infinite restart loops
* Unhandled promise rejections
* Random `process.exit(1)`
* No context, no discipline

**zero-crash** gives your app a **runtime safety contract**.

✔ Zero dependencies
✔ Global crash interception
✔ Clean exit codes
✔ Shutdown hooks
✔ Context-aware crash logs
✔ Works for APIs, CLIs, bots, servers

---

## 📦 Installation

```bash
npm install zero-crash
```

---

## 🧠 Basic Usage

```js
const zero = require("zero-crash");

zero.protect(async () => {
  // your app logic
  startServer();
});
```

That’s it.
Global crash protection is now active.

---

## 🔥 Advanced Usage (Recommended)

### 🧩 Role Awareness

```js
zero.role("api");
```

Crash output will include role:

```
💥 [api] RUNTIME_ERROR
```

---

### 🔐 Environment Validation

```js
zero.requireEnv(["PORT", "DB_URL"]);

zero.protect(async () => {
  startServer();
});
```

If missing:

```
💥 [app] CONFIG_ERROR
Missing env: DB_URL
Exit: 2
```

---

### 🛑 Safe Shutdown Hooks

```js
zero.onShutdown(async () => {
  await db.close();
  await redis.quit();
});
```

Runs on:

* crash
* Ctrl+C
* SIGTERM
* process exit

---

### ⚠️ Crash Classification

```js
throw zero.config("Invalid configuration");
throw zero.dependency("MongoDB not reachable");
```

Mapped exit codes:

| Type             | Exit Code |
| ---------------- | --------- |
| Success          | `0`       |
| Runtime Error    | `1`       |
| Config Error     | `2`       |
| Dependency Error | `3`       |
| Manual Interrupt | `130`     |

---

### 🧪 Full Example

```js
const zero = require("zero-crash");

zero.role("bot");
zero.requireEnv(["SESSION"]);

zero.onShutdown(async () => {
  console.log("Cleaning up...");
});

zero.protect(async () => {
  throw zero.config("SESSION missing");
});
```

---

## 🪄 Crash Output Example

```
💥 [bot] CONFIG_ERROR
Reason: SESSION missing
Exit: 2
CrashID: ZC-A91F2B
Node: v20.11.1
Memory: 42MB
Uptime: 12s
```

---

## ⚙️ Options

```js
zero.protect(app, {
  verbose: false,
  quiet: false,
  json: false,
  onCrash: (err, meta) => {
    // send to webhook / logs
  }
});
```

| Option    | Description               |
| --------- | ------------------------- |
| `verbose` | Show full stack trace     |
| `quiet`   | Disable console logs      |
| `json`    | Output crash info as JSON |
| `onCrash` | Custom crash hook         |

---

## 🛠️ Use Cases

* REST APIs
* CLI tools
* WhatsApp / Telegram bots
* Cron jobs
* Microservices
* Workers & daemons

If it runs on Node.js, **zero-crash** belongs there.

---

## ⭐ Support the Project

If this package improved your app’s stability:

👉 **Give it a ⭐ on GitHub**
Stars help this project reach more developers ❤️

---

## 🔄 Updates & Contributions

Want to improve `zero-crash`?

* 🐞 Found a bug? → **Open an Issue**
* ✨ Feature idea? → **Create an Issue**
* 🔧 Fix something? → **Fork & Pull Request**
* 📈 Improvements welcome

Please contribute only through the **official repository**.

---

## 📜 License

MIT License © 2026
**Abhishek Suresh**
[https://github.com/AbhishekSuresh2](https://github.com/AbhishekSuresh2)

> ⚠️ Please do not copy, rebrand, or republish this package as your own without explicit permission.

---

## 🌍 Vision for 2026

Failures are inevitable.
Chaos is optional.

**zero-crash** makes crashes **predictable, readable, and safe** —
so your app never dies silently again 💥🛡️
