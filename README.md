# 🪨 pebble

> A tiny, dependency-free debug logger for Node.js and browsers.

`pebble` is a minimal clone of the popular [`debug`](https://www.npmjs.com/package/debug) library — rebuilt from scratch with **zero dependencies**.  
It supports **namespaces**, **colorized output**, **wildcard patterns**, and **time deltas** — all in less than 2 KB of code.

## Features

- **Zero dependencies** — pure TypeScript / ES module  
- **Colorized output** (ANSI for Node, `%c` in browsers)  
- **Namespace & pattern filtering** (`DEBUG=app:*,-app:noise`)  
- **Time difference** between calls  
- **Works everywhere** — Node, Deno, Browser  
- **Tiny footprint** — ~150 lines, < 2 KB  

## Installation

```bash
npm install pebble
# or
pnpm add pebble
# or
yarn add pebble
```

## Usage

### Enable via environment or localStorage

```bash
# Enable all namespaces
DEBUG="*"

# Enable specific namespaces
DEBUG="app:*,db"

# Exclude noisy ones
DEBUG="app:*, -app:noise"
```

In browsers:

```js
localStorage.DEBUG = 'app:*,-app:noise';
```

---

### Example

```ts
import createDebug, { enable } from "pebble";

// Enable manually if not using env vars
enable("app:*, -app:noise");

const log = createDebug("app");
const api = log.extend("api");
const db  = log.extend("db");

log("booting app on port", 3000);
api("GET /users", { page: 1 });
db("connected in %dms", 42);
```

## API

### `createDebug(namespace: string): DebugFn`
Creates a new logger for a specific namespace.

### `enable(patterns: string): void`
Glob-style pattern matching.  
Example: `"app:*, -app:noise"`

### `disable(): void`
Disables all loggers.

### `enabled(namespace: string): boolean`
Checks if a namespace is currently active.

### `debug.extend(sub: string): DebugFn`
Creates a sub-namespace logger (e.g. `app:db` → `app:db:query`).

---

## Philosophy

> “A pebble is small but solid.”

`pebble` is built on one principle: **visibility should not depend on weight**.  
It’s perfect for:

- Libraries that can’t afford heavy dependencies
- Microservices and edge runtimes
- Lightweight frontends
- Teaching and debugging minimal environments

## Example Setup

**package.json**

```json
{
  "name": "pebble",
  "version": "1.0.0",
  "main": "dist/index.js",
  "types": "dist/index.d.ts",
  "scripts": {
    "build": "tsc",
    "test": "node examples/basic.js"
  },
  "files": ["dist"]
}
```

## 🧑‍💻 Contributing

PRs are welcome!  
If you spot a bug or want to add a small feature, open an issue first to keep the core minimal.  

```bash
pnpm install
pnpm build
pnpm test
```

## 🪪 License

MIT © 2025 [Jean Burellier](https://github.com/sheplu)

> 💬 *"Every big log starts with a small pebble."*
