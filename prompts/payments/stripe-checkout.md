# Stripe Subscription Checkout API Route

## Context
You need a Next.js API route that creates a Stripe Checkout session for subscriptions.  
It should fetch the logged-in Clerk user, link them to the Neon DB, and create/manage Stripe customer IDs.

## Prompt
Generate a Next.js 15 App Router route handler at `/api/checkout` that:
- Uses Clerk to get the logged-in user
- Checks if the user exists in Neon DB (via Drizzle), else inserts
- Creates or reuses Stripe customer
- Creates a Checkout session for subscription plan `planId` passed in the request body
- Returns the `url` to redirect

## Example AI Output
```ts
// app/api/checkout/route.ts
import { auth } from "@clerk/nextjs";
import { db } from "@/db";
import { users } from "@/db/schema";
import Stripe from "stripe";

const stripe = new Stripe(process.env.STRIPE_SECRET_KEY!, { apiVersion: "2024-06-20" });

export async function POST(req: Request) {
  const { userId } = auth();
  if (!userId) return new Response("Unauthorized", { status: 401 });

  const { planId } = await req.json();

  let user = await db.query.users.findFirst({ where: (u) => u.clerkId.eq(userId) });

  if (!user) {
    user = await db.insert(users).values({ clerkId: userId, email: "" }).returning().get();
  }

  const customer = await stripe.customers.create({ email: user.email, metadata: { userId } });

  const session = await stripe.checkout.sessions.create({
    mode: "subscription",
    customer: customer.id,
    line_items: [{ price: planId, quantity: 1 }],
    success_url: `${process.env.NEXT_PUBLIC_URL}/dashboard?success=1`,
    cancel_url: `${process.env.NEXT_PUBLIC_URL}/pricing?canceled=1`,
  });

  return Response.json({ url: session.url });
}
```