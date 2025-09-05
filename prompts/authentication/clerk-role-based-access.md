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
import { authMiddleware, redirectToSignIn } from "@clerk/nextjs";

export default authMiddleware({
  publicRoutes: ["/", "/pricing", "/api/webhooks(.*)"],
  afterAuth(auth, req) {
    if (req.nextUrl.pathname.startsWith("/admin")) {
      if (!auth.userId || auth.sessionClaims?.metadata?.role !== "admin") {
        return redirectToSignIn({ returnBackUrl: req.url });
      }
    }
  },
});

export const config = {
  matcher: ["/((?!.*\..*|_next).*)"],
};
```