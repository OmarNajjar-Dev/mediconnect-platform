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

## Project Structure

```
frontend-next/
├─ src/
│  └─ app/
│     ├─ layout.tsx
│     ├─ page.tsx
│     └─ globals.css
├─ next.config.ts
├─ tsconfig.json
└─ eslint.config.mjs
```

## UI: shadcn/ui

Initialize and generate components after Tailwind is configured:

```bash
npx shadcn@latest init
npx shadcn@latest add button card dialog input
```

Components will be generated under `src/components` (or the configured path). Ensure Tailwind is enabled and `globals.css` includes the required base layers.

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

Environment variables are managed via Next.js runtime config. Create `.env.local` for local overrides as needed.
