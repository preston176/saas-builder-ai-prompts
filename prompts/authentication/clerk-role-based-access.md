# Clerk Role-Based Access Middleware

## Context

You have a SaaS with multiple user roles (admin, user, support).  
You want to protect routes in Next.js 15 using Clerk middleware and allow only admins to access `/admin`.

## Prompt

I’m using **Next.js 15 with App Router** and **Clerk** for authentication.  
Generate a `middleware.ts` that:

- Protects all routes by default
- Allows public access to `/`, `/pricing`, and `/api/webhooks/*`
- Restricts `/admin` to only users with role = "admin" in Clerk metadata

## Example AI Output

```ts
// middleware.ts
import { clerkMiddleware, createRouteMatcher } from "@clerk/nextjs/server";

const isPublicRoute = createRouteMatcher(["/auth(.*)", "/", "/help"]);

export default clerkMiddleware(async (auth, req) => {
  if (!isPublicRoute(req)) {
    await auth.protect();
  }
});

export const config = {
  matcher: [
    // Skip Next.js internals and all static files, unless found in search params
    "/((?!_next|[^?]*\\.(?:html?|css|js(?!on)|jpe?g|webp|png|gif|svg|ttf|woff2?|ico|csv|docx?|xlsx?|zip|webmanifest)).*)",
    // Always run for API routes
    "/(api|trpc)(.*)",
  ],
};
```
