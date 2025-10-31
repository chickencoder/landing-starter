# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Next.js 16 landing page starter built with:
- **Next.js 16.0.1** with App Router and React Server Components (RSC)
- **React 19.2.0**
- **TypeScript 5** with strict mode enabled
- **Tailwind CSS v4** (using the new @tailwindcss/postcss plugin)
- **shadcn/ui** components with "new-york" style
- **Custom landing component registry** at `https://registry-inky-xi.vercel.app/r/{name}.json`

## Development Commands

**Package manager**: pnpm (lockfile present)

```bash
# Start development server (http://localhost:3000)
pnpm dev

# Build for production
pnpm build

# Start production server
pnpm start

# Run ESLint
pnpm lint
```

## Architecture

### Styling System

The project uses **Tailwind CSS v4** which has significant differences from v3:

- No `tailwind.config.ts` file at root - configuration is in `app/globals.css` using `@theme inline`
- Uses PostCSS plugin `@tailwindcss/postcss` instead of standalone Tailwind
- Custom CSS variables defined in `:root` and `.dark` selectors
- Color system uses OKLCH color space for better perceptual uniformity
- Custom variant for dark mode: `@custom-variant dark (&:is(.dark *))`
- Includes `tw-animate-css` for additional animation utilities

### Component System

The project is configured for shadcn/ui components with a **custom registry**:

- Primary registry: `@landing` → `https://registry-inky-xi.vercel.app/r/{name}.json`
- Component aliases configured in `components.json`:
  - `@/components` → components directory
  - `@/ui` → components/ui directory
  - `@/lib` → lib directory
  - `@/utils` → lib/utils
  - `@/hooks` → hooks directory
- Path alias `@/*` maps to project root (configured in `tsconfig.json`)
- Style: "new-york" variant
- Icon library: lucide-react
- Base color: neutral
- Using CSS variables for theming

**Note**: When adding shadcn components, they will be fetched from the custom `@landing` registry. The components directory will be created on first component addition.

### Utilities

- `lib/utils.ts` provides the `cn()` function for conditional className merging using `clsx` and `tailwind-merge`
- Use this for all dynamic className composition

### Fonts

The app uses Vercel's Geist font family:
- `Geist` (sans-serif) via `--font-geist-sans` variable
- `Geist Mono` (monospace) via `--font-geist-mono` variable
- Both are auto-optimized via `next/font/google`

### TypeScript Configuration

- Target: ES2017
- Strict mode enabled
- Path alias: `@/*` → root directory
- JSX runtime: react-jsx (React 19)
- Module resolution: bundler

## Project Structure

```
app/
  ├── layout.tsx       # Root layout with font configuration
  ├── page.tsx         # Home page
  └── globals.css      # Tailwind v4 theme configuration
lib/
  └── utils.ts         # cn() utility for className merging
components/            # Created when first shadcn component is added
  └── ui/              # shadcn/ui components location
```

## Important Notes

- This uses **Tailwind CSS v4**, not v3. Do not create a `tailwind.config.ts` file - use the `@theme inline` directive in `app/globals.css` instead
- Components from `@landing` registry may have custom implementations - review them before modifying
- Dark mode uses a custom variant that requires the `.dark` class on a parent element
- The project uses React 19's new JSX runtime - no need to import React in files
