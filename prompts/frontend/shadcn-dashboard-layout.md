# Shadcn Dashboard Layout with Sidebar + Topbar

## Context
You need a modern SaaS dashboard layout with a sidebar for navigation and a topbar for user profile/avatar.  
It should use Shadcn UI + Tailwind.

## Prompt
Generate a responsive SaaS dashboard layout in Next.js 15 with:
- A collapsible sidebar (`Dashboard`, `Billing`, `Settings`)
- A topbar with Clerk user avatar dropdown
- Dark mode support
- Mobile-first design

## Example AI Output
```tsx
"use client";

import { useState } from "react";
import { Avatar, AvatarFallback, AvatarImage } from "@/components/ui/avatar";
import { Button } from "@/components/ui/button";
import { Menu } from "lucide-react";

export default function DashboardLayout({ children }: { children: React.ReactNode }) {
  const [open, setOpen] = useState(false);

  return (
    <div className="flex h-screen">
      {/* Sidebar */}
      <aside className={`bg-gray-900 text-white p-4 ${open ? "w-64" : "w-16"} transition-all`}>
        <Button variant="ghost" size="icon" onClick={() => setOpen(!open)}>
          <Menu className="h-6 w-6" />
        </Button>
        <nav className="mt-6 space-y-4">
          <a href="/dashboard">Dashboard</a>
          <a href="/billing">Billing</a>
          <a href="/settings">Settings</a>
        </nav>
      </aside>

      {/* Main */}
      <main className="flex-1 flex flex-col">
        <header className="flex items-center justify-end p-4 border-b">
          <Avatar>
            <AvatarImage src="https://github.com/shadcn.png" />
            <AvatarFallback>U</AvatarFallback>
          </Avatar>
        </header>
        <div className="flex-1 p-6">{children}</div>
      </main>
    </div>
  );
}
```