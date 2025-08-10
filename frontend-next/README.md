# MediConnect Frontend — Next.js + TypeScript + shadcn/ui

This folder contains the MediConnect frontend built with Next.js (App Router), TypeScript, Tailwind CSS, and shadcn/ui. Unit tests are planned with Jest and Testing Library.

## Stack

- Next.js 15 (React 19)
- TypeScript 5
- Tailwind CSS 4
- shadcn/ui (Radix UI primitives)
- Jest + Testing Library (planned)

## Scripts

```bash
npm run dev      # Start dev server (http://localhost:3000)
npm run build    # Production build
npm run start    # Start production server
npm run lint     # Lint with ESLint
```

## Getting Started

```bash
cd frontend-next
npm install
npm run dev
```

Open http://localhost:3000 in your browser. Edit `src/app/page.tsx` to start.

## Project Structure (features-first, simple & flexible)

```
frontend-next/
├─ public/
├─ src/
│  ├─ app/                      # App Router (server components by default)
│  │  ├─ layout.tsx
│  │  ├─ page.tsx
│  │  └─ globals.css
│  ├─ features/                 # Primary unit (by domain)
│  │  ├─ doctors/
│  │  │  ├─ components/
│  │  │  ├─ api.ts             # Feature API calls
│  │  │  ├─ types.ts
│  │  │  └─ index.ts           # Re-exports (public surface)
│  │  └─ appointments/
│  ├─ components/
│  │  └─ ui/                    # shadcn/ui generated components
│  ├─ lib/
│  │  ├─ api.ts                 # HTTP client (fetch wrapper)
│  │  └─ utils.ts
│  └─ types/                    # Global shared types
├─ jest.config.ts               # Optional testing config
├─ jest.setup.ts                # Optional testing setup
├─ next.config.ts
├─ tsconfig.json
├─ eslint.config.mjs
└─ .env.local.example           # Example envs (no secrets)
```

Best practices:

- Co-locate code by feature. Expose a stable public API via each feature's `index.ts`.
- Shared primitives go in `src/components/ui` (shadcn/ui) or `src/components`.
- Use path aliases (e.g., `@/features/...`) to avoid long relative imports.
- Prefer server components for data fetching; use client components only where interactivity is required.

MVC mapping (Next.js context):

- Model: backend data contracts and feature `types.ts`
- View: React components in `app/` and `components/`
- Controller: server actions or route handlers orchestrating API calls

### Path Aliases

`tsconfig.json` excerpt:

```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"]
    }
  }
}
```

## UI: shadcn/ui

Initialize and generate components after Tailwind is configured:

```bash
npx shadcn@latest init
npx shadcn@latest add button card dialog input
```

Components will be generated under `src/components` (or the configured path). Ensure Tailwind is enabled and `globals.css` includes the required base layers.

## API Integration (consuming Laravel)

Set the backend URL in `.env.local`:

```ini
NEXT_PUBLIC_API_URL=http://localhost:8000
```

Create `src/lib/api.ts`:

```ts
export const API_BASE_URL =
  process.env.NEXT_PUBLIC_API_URL ?? "http://localhost:8000";

export async function apiRequest<T>(
  path: string,
  init: RequestInit = {}
): Promise<T> {
  const res = await fetch(`${API_BASE_URL}${path}`.replace(/\/$/, ""), {
    credentials: "include", // if using cookie-based auth
    headers: { "Content-Type": "application/json", ...(init.headers || {}) },
    ...init,
  });
  if (!res.ok) throw new Error(`API ${res.status}: ${await res.text()}`);
  return res.json() as Promise<T>;
}
```

Example (server component, acts as controller):

```ts
type Doctor = { id: string; name: string; specialty: string };

export default async function DoctorsPage() {
  const doctors = await apiRequest<Doctor[]>(`/api/v1/doctors`);
  return (
    <ul>
      {doctors.map((d) => (
        <li key={d.id}>{d.name}</li>
      ))}
    </ul>
  );
}
```

Example (client component):

```ts
"use client";
import { useEffect, useState } from "react";

type Doctor = { id: string; name: string };

export function DoctorsList() {
  const [data, setData] = useState<Doctor[]>([]);
  useEffect(() => {
    apiRequest<Doctor[]>("/api/v1/doctors").then(setData);
  }, []);
  return (
    <ul>
      {data.map((d) => (
        <li key={d.id}>{d.name}</li>
      ))}
    </ul>
  );
}
```

Notes:

- Ensure CORS in Laravel allows `http://localhost:3000` and your Vercel domain.
- Use `/api/v1/*` endpoints; keep API responses stable using Laravel Resources.

## Testing (Jest) — optional setup

Install dev dependencies:

```bash
npm i -D jest ts-jest @types/jest jest-environment-jsdom \
  @testing-library/react @testing-library/jest-dom @testing-library/user-event
```

Add a basic config (e.g., `jest.config.ts`):

```ts
import type { Config } from "jest";

const config: Config = {
  testEnvironment: "jest-environment-jsdom",
  transform: { "^.+\\.(ts|tsx)$": ["ts-jest", { tsconfig: "tsconfig.json" }] },
  moduleNameMapper: { "^@/(.*)$": "<rootDir>/src/$1" },
  setupFilesAfterEnv: ["<rootDir>/jest.setup.ts"],
};
export default config;
```

And `jest.setup.ts`:

```ts
import "@testing-library/jest-dom";
```

Then run:

```bash
npx jest
```

## Linting & Formatting

```bash
npm run lint
```

## Environment

Environment variables are managed via Next.js runtime config. Create `.env.local` for local overrides:

```ini
NEXT_PUBLIC_API_URL=http://localhost:8000
```

## Deployment (Vercel)

- Connect this repo/folder in Vercel
- Set `NEXT_PUBLIC_API_URL` to the backend URL (e.g., Railway domain)
- Vercel auto-detects Next.js and builds with `next build`
