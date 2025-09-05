# Bun Setup for Next.js SaaS

## Context
You’re using Bun instead of Node.js to run your Next.js 15 SaaS.  
You need a `package.json` + scripts that run the dev server, build, and start.

## Prompt
Generate Bun config for a Next.js 15 project that:
- Uses Bun as runtime
- Includes scripts for dev, build, start
- Ensures Stripe webhooks run correctly
- Works with Neon and Drizzle

## Example AI Output
```json
{
  "scripts": {
    "dev": "bun run next dev",
    "build": "bun run next build",
    "start": "bun run next start",
    "lint": "bun run next lint",
    "stripe:webhook": "bunx stripe listen --forward-to localhost:3000/api/webhooks/stripe"
  }
}
```