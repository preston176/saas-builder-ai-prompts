# 🚀 SaaS Prompts  
**AI-Powered Prompts for Building SaaS Faster with Next.js 15, Clerk, Stripe, Neon & Drizzle**  

> Stop reinventing the wheel. This repo is a **curated collection of prompts** you can use with ChatGPT, Claude, or any LLM to build SaaS products—end to end.  

---

## 🔹 Why This Repo?
Building SaaS is hard. You need to set up authentication, databases, payments, dashboards, and deployment—fast.  
With the right prompts, you can skip boilerplate struggles and **ship faster**.  

This repo collects **battle-tested prompts** for the modern SaaS stack:  

- ⚡ **Next.js 15** (App Router + Server Components)  
- 🔑 **Clerk** (Authentication & RBAC)  
- 💳 **Stripe** (Payments & Subscriptions)  
- 🛢️ **Neon + Drizzle ORM** (Database & Migrations)  
- 🟣 **Bun** (Fast runtime & tooling)  

---

## 📂 Structure
Prompts are organized by SaaS essentials:

```
prompts/
├── authentication/   → Clerk setup, RBAC, protected routes
├── database/         → Neon setup, Drizzle schemas, migrations
├── backend/          → Next.js API routes, Bun runtime setup
├── payments/         → Stripe integration, subscriptions, webhooks
├── frontend/         → Dashboards, Shadcn UI, server components
├── devops/           → Deployment, monitoring, scaling
├── marketing/        → Landing pages, SEO, growth
└── misc/             → AI productivity, debugging, boilerplate
```

---

## ✨ Example Prompt
```md
# Clerk Authentication Setup

## Prompt
I am building a SaaS platform using Next.js 15 and Clerk.  
Generate the setup code to initialize Clerk, configure middleware, and protect routes.  
Make sure it supports server components and API routes.
```

**Sample Output:**
```ts
// middleware.ts
import { authMiddleware } from "@clerk/nextjs";

export default authMiddleware({ publicRoutes: ["/"] });

export const config = {
  matcher: ["/((?!_next|.*\..*).*)"],
};
```

---

## 🚀 How to Use
1. Pick a prompt from the relevant folder.  
2. Paste it into your LLM (ChatGPT, Claude, Cursor, Copilot, etc.).  
3. Copy the generated code into your SaaS project.  
4. Iterate and ship 🚀.  

---

## 🤝 Contributing
Want to add a new SaaS prompt? PRs are welcome!  

- Check the [contributing guide](CONTRIBUTING.md)  
- Open an issue with **Prompt Request** label  
- Add your prompt in the correct category  

All contributors will be featured on the repo wall ⭐.  

---

## 📈 Roadmap
- [ ] Add 100+ prompts (MVP goal)  
- [ ] Launch on Product Hunt  
- [ ] Add a website with searchable prompts  
- [ ] CLI tool: `npx saas-prompts stripe subscription`  

---

## 🏷️ Tags & Topics
`saas` · `nextjs` · `stripe` · `clerk` · `drizzle` · `neon` · `bun` · `prompts` · `ai`  

---

## ⭐ Support
If this repo saves you time, give it a star ⭐ and share it with other builders!  
