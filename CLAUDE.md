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

**Package manager**: npm

```bash
# Start development server (http://localhost:3000)
npm run dev

# Build for production
npm run build

# Start production server
npm start

# Run ESLint
npm run lint
```

## Key Architecture Notes

- **App Router with RSC**: Components are server components by default
- **React 19 JSX runtime**: No need to import React in files
- **Tailwind CSS v4**: Configuration in `app/globals.css` using `@theme inline` directive (no `tailwind.config.ts` file)
- **Custom shadcn registry**: Components from `@landing` registry at `https://registry-inky-xi.vercel.app/r/{name}.json`
- **Path alias**: `@/*` maps to project root (configured in `tsconfig.json`)

## Building Pages

For detailed guidance on creating landing pages and multi-page websites, see:

📄 **`.claude/skills/page-builder/SKILL.md`**

This includes:
- Step-by-step process for building pages
- Component discovery and usage from `@landing` and `@react-bits` registries
- Design system implementation
- Tailwind v4 configuration details
- Conversion optimization strategies
- Design decision framework by business type
