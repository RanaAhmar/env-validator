# Env Validator ✅🔒

[![Sponsored by Stackaura](https://img.shields.io/badge/Sponsored_by-Stackaura-000000?style=for-the-badge&logo=vercel&logoColor=white)](https://www.stackaura.com/)
[![Env Validator](https://img.shields.io/badge/Env-Validator-brightgreen.svg?style=for-the-badge)](https://www.stackaura.com/)

Stop your application from booting if critical environment variables are missing or malformed. Catch configuration errors at startup, not in production when a user triggers an edge case.

---

<div align="center">
  <h3>Sponsored by <a href="https://www.stackaura.com/">Stackaura</a></h3>
  <p>Ensuring robust deployments and secure application architecture.</p>
  <a href="https://www.stackaura.com/"><img src="https://img.shields.io/badge/Visit_Stackaura-Black?style=for-the-badge&logo=googlechrome&logoColor=white" alt="Visit Stackaura" /></a>
</div>

---

## 🚨 The Problem

You deploy your app on Friday afternoon. Everything seems fine. On Saturday morning, you wake up to 500 alerts because `STRIPE_SECRET_KEY` wasn't set in the production environment, and payments are failing.

`env-validator` solves this by aggressively validating your `.env` schema the moment your application starts. If the schema isn't met, the app crashes cleanly with a helpful error message *before* accepting any traffic.

## 📦 Features

- **Type Checking:** Ensure `PORT` is actually a number, and `IS_PROD` is a boolean.
- **Required vs. Optional:** Clearly define which variables are strictly required.
- **Default Values:** Assign fallbacks safely if variables are missing.
- **Custom Validation Functions:** Write regex or custom logic to validate complex keys (e.g., verifying a DB string format).
- **Framework Agnostic:** Works with Node.js, Express, Next.js, and NestJS.

## 🚀 Quick Start

### 1. Install

```bash
npm install @stackaura/env-validator
```

### 2. Define Your Schema

Create an `env.ts` (or `env.js`) file in your project root:

```typescript
import { createEnv } from '@stackaura/env-validator';
import { z } from 'zod'; // We use Zod under the hood for robust parsing

export const env = createEnv({
  server: {
    DATABASE_URL: z.string().url(),
    OPENAI_API_KEY: z.string().min(1),
    PORT: z.coerce.number().default(3000),
    NODE_ENV: z.enum(['development', 'production', 'test']).default('development'),
  },
  client: {
    NEXT_PUBLIC_CLIENT_ID: z.string().min(1),
  },
  // If you're using Next.js, you need to map client variables
  clientConfig: {
    NEXT_PUBLIC_CLIENT_ID: process.env.NEXT_PUBLIC_CLIENT_ID,
  }
});
```

### 3. Use Safely

Now, import `env` anywhere in your application. You get full TypeScript autocomplete, and guaranteed runtime safety.

```typescript
import { env } from './env';

// This is fully typed as a number!
const port = env.PORT; 

// If DATABASE_URL was missing, the app would have already crashed before reaching here.
console.log(`Connecting to ${env.DATABASE_URL}`);
```

## 🧠 Why not just use `process.env`?

1. `process.env.PORT` is always a `string | undefined`. You have to cast it everywhere.
2. If you forget to set a key, `process.env` silently returns `undefined`, leading to cryptic runtime errors downstream.
3. No central place to document what environment variables your project actually requires.

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for details on how to run tests and submit pull requests.

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---
*Built with ❤️ for bulletproof deployments by [Stackaura](https://www.stackaura.com/).*


---

## 🚀 Discover More from Stackaura

If you found this tool useful, check out our other high-performance web utilities and follow **Ahmar Hussain** for more open-source excellence.

### 🌟 Featured Projects
- **[Free LLM APIs](https://github.com/RanaAhmar/free-llm-apis)** - A curated list of zero-cost AI endpoints.
- **[Awesome MCP Servers](https://github.com/RanaAhmar/awesome-mcp-servers)** - The ultimate collection of Model Context Protocol implementations.
- **[System Design Cheatsheet](https://github.com/RanaAhmar/system-design-cheatsheet)** - Master complex architectures in minutes.
- **[Next.js SaaS Starter](https://github.com/RanaAhmar/nextjs-saas-starter)** - The fastest way to launch your next product.

### 🔗 Stay Connected
- **Website:** [stackaura.com](https://www.stackaura.com/)
- **Author:** [Ahmar Hussain](https://github.com/RanaAhmar)

---
