# Drizzle Schema for SaaS Subscriptions

## Context
You’re using Neon (Postgres) with Drizzle ORM.  
You need a schema for users, subscriptions, and plans that works with Stripe integration.

## Prompt
Generate a Drizzle schema for:
- `users` table → id, clerkId, email
- `plans` table → id, name, price, interval
- `subscriptions` table → id, userId, planId, stripeSubId, status, currentPeriodEnd
Make sure to use Neon-compatible Drizzle syntax.

## Example AI Output
```ts
import { pgTable, uuid, text, timestamp, integer } from "drizzle-orm/pg-core";

export const users = pgTable("users", {
  id: uuid("id").defaultRandom().primaryKey(),
  clerkId: text("clerk_id").notNull().unique(),
  email: text("email").notNull().unique(),
});

export const plans = pgTable("plans", {
  id: uuid("id").defaultRandom().primaryKey(),
  name: text("name").notNull(),
  price: integer("price").notNull(),
  interval: text("interval", { enum: ["month", "year"] }).notNull(),
});

export const subscriptions = pgTable("subscriptions", {
  id: uuid("id").defaultRandom().primaryKey(),
  userId: uuid("user_id").notNull().references(() => users.id),
  planId: uuid("plan_id").notNull().references(() => plans.id),
  stripeSubId: text("stripe_sub_id").notNull().unique(),
  status: text("status", { enum: ["active", "canceled", "trialing"] }).notNull(),
  currentPeriodEnd: timestamp("current_period_end", { withTimezone: true }),
});
```