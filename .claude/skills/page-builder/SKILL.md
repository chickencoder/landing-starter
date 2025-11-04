---
name: page-builder
description: For creating page or updating existing code
---

# Page Builder

Build high-end, visually stunning, conversion-focused landing pages using modern web technologies.

## Quick Workflow Checklist

- [ ] Discover components with `mcp__shadcn__search_items_in_registries`
- [ ] Add components with the CLI command
- [ ] **READ each component file to see actual exports** ⚠️
- [ ] Add navbar first (search for "nav" in `@landing`)
- [ ] Build page sections
- [ ] Never assume component names - always verify

## Tech Stack

- **Next.js 16.0.1** with App Router and React Server Components (RSC)
- **React 19.2.0** (no React imports needed - uses new JSX runtime)
- **TypeScript 5** with strict mode
- **Tailwind CSS v4** (config in `app/globals.css`, not separate config file)
- **shadcn/ui** with custom registries:
  - `@landing` → Landing page components
  - `@react-bits` → Backgrounds and animations

## Step-by-Step Process

### 1. Planning & Design

Before building, consider:

- **Design patterns**: What layouts and features match the use case?
- **Call to action**: What's the primary conversion goal? (button, form, signup)
- **Business type**: SaaS/tech (modern, animated) vs e-commerce (clean, product-focused) vs local business (photo-heavy)
- **Style direction**: Colors, fonts, border radius, shadows, overall feel

### 2. Discover Available Components

List components from registries:

```bash
# Use shadcn MCP tool to see what's available
mcp__shadcn__list_items_in_registries
```

Search for specific patterns:

```bash
# Search for components by name or description
mcp__shadcn__search_items_in_registries
```

Key component types in `@landing`:

- Sections (hero, features, pricing, testimonials, CTA)
- Navigation components
- Footer components
- Form components

Key component types in `@react-bits`:

- Animated backgrounds
- Visual effects
- Interactive elements

### 3. Add Components to Project

Get the add command for selected components:

```bash
# Get the CLI command to add components
mcp__shadcn__get_add_command_for_items
```

Then run the returned command (typically `npx shadcn add ...`).

**⚠️ CRITICAL - Before writing ANY code:**

```bash
# Read each component file you added
Read tool: components/hero-01.tsx
Read tool: components/pricing-01.tsx
# etc.
```

Document the actual exports. Don't assume naming - components may use `CallOut01` (capital O), `CardName` (not CardTitle), or expect external UI components like `Avatar`.

### 4. Implement Layout (Navbar & Footer)

**⚠️ ALWAYS add navbar first** (unless told otherwise). Every landing page needs navigation.

1. Search: `mcp__shadcn__search_items_in_registries` with "nav" or "header"
2. Add component → **Read the file** → Implement in `app/layout.tsx`
3. Then build page content

**Unless instructed otherwise**, implement navigation and footer in `app/layout.tsx`:

- Use components from `@landing` registry
- Match the overall design style
- Ensure responsive behavior
- Add navigation links for all pages

### 5. Build Pages

Create pages in the `app/` directory:

```
app/
├── layout.tsx       # Root layout (navbar + footer)
├── page.tsx         # Home page
├── about/
│   └── page.tsx     # About page
└── pricing/
    └── page.tsx     # Pricing page
```

**Page structure**:

- Use section components from `@landing` registry
- Combine multiple sections for complete pages
- Add backgrounds and animations from `@react-bits` for visual interest
- Implement conversion-focused copy and CTAs

**Important**: Components from `@landing` are designed to be composed with other UI elements around them - they're building blocks, not full templates.

### 6. Style & Theme

Configure design system in `app/globals.css`:

**Tailwind v4 specifics**:

- ✅ Configuration uses `@theme inline` directive (no separate config file)
- ✅ Define colors, fonts, border radius, shadows in CSS
- ✅ Uses OKLCH color space for better color uniformity
- ✅ CSS variables for theming (`--color-*` variables)
- ✅ Dark mode via `.dark` class on parent element

**Fonts**: Use Google Fonts

```css
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap");

@theme inline {
  --font-sans: "Inter", system-ui, sans-serif;
}
```

**Colors**: Define using OKLCH and CSS variables

```css
:root {
  --color-primary: oklch(0.6 0.2 250);
  --color-accent: oklch(0.7 0.15 180);
}
```

**Design tokens**: Border radius, shadows, spacing

```css
@theme inline {
  --radius-sm: 0.25rem;
  --radius-md: 0.5rem;
  --radius-lg: 1rem;
}
```

### 7. Conversion Optimization

**Call to Action**:

- Make primary CTA highly visible (contrasting color, prominent placement)
- Use action-oriented copy ("Start Free Trial" > "Learn More")
- Place CTAs above the fold and at natural break points

**Social Proof**:

- Customer testimonials with photos
- Company logos (clients/partners)
- Usage statistics ("10,000+ users")
- Trust badges and certifications

**Copy Guidelines**:

- Conversion-focused headlines (problem → solution)
- Benefit-driven (outcomes, not features)
- Consistent message throughout page
- Clear value proposition

## Design System

### Backgrounds & Animations

Use `@react-bits` for visual interest:

- Animated gradients
- Particle effects
- Parallax backgrounds
- Scroll-triggered animations

Apply these to sections to create depth and engagement.

### Component Composition

`@landing` components are building blocks:

```tsx
// ✅ Good: Compose with other elements
<HeroSection>
  <CustomBadge />
  <Heading />
  <CTAButton />
</HeroSection>

// ❌ Avoid: Using components as-is without customization
<HeroSection />
```

### Theming

Use shadcn color system with CSS variables:

```css
:root {
  --background: 0 0% 100%;
  --foreground: 222.2 84% 4.9%;
  --primary: 221.2 83.2% 53.3%;
}

.dark {
  --background: 222.2 84% 4.9%;
  --foreground: 210 40% 98%;
  --primary: 217.2 91.2% 59.8%;
}
```

Apply in components using Tailwind utilities:

```tsx
<div className="bg-background text-foreground">
```

## Design Decision Framework

### SaaS / Tech Products

- ✅ Lots of visual effects and animations
- ✅ Shadows, gradients, glows
- ✅ Rounded corners (modern feel)
- ✅ Bold, contrasting colors
- ✅ Animated backgrounds from `@react-bits`

### In-Person / Local Businesses

- ✅ Real photographs (team, location, customers)
- ✅ Authentic, trust-building imagery
- ✅ Clear contact information
- ✅ Location/hours prominent
- ⚠️ Less emphasis on animations

### E-commerce

- ✅ Sharp corners (professional, clean)
- ✅ High-quality product photography
- ✅ Clear product hierarchy
- ✅ Simple, uncluttered design
- ✅ Focus on products, not decorative elements
- ⚠️ Minimal animations (don't distract from products)

## Technical Notes

### Tailwind CSS v4 Differences

**No `tailwind.config.ts` file** - configuration is in `app/globals.css`:

```css
@import "tailwindcss";

@theme inline {
  /* Your theme config here */
}
```

**Dark mode** uses custom variant:

```css
@custom-variant dark (&:is(.dark *));
```

Requires `.dark` class on a parent element to activate.

### React 19 & Next.js 16

- **No React imports needed**: React 19 JSX runtime handles this
- **Server Components by default**: Add `"use client"` for interactivity
- **Async components**: Server Components can be async

```tsx
// ✅ Server Component (default)
export default async function Page() {
  const data = await fetchData();
  return <div>{data}</div>;
}

// ✅ Client Component (for interactivity)
("use client");
export default function InteractiveComponent() {
  const [state, setState] = useState(0);
  return <button onClick={() => setState(state + 1)}>{state}</button>;
}
```

### Path Aliases

Configured in `tsconfig.json` and `components.json`:

```tsx
import { Button } from "@/components/ui/button"; // ✅
import { cn } from "@/lib/utils"; // ✅
import { useHook } from "@/hooks/use-hook"; // ✅
```

### Utility Functions

Use `cn()` from `@/lib/utils` for conditional className merging:

```tsx
import { cn } from "@/lib/utils";

<div className={cn("base-class", isActive && "active-class", className)} />;
```

## Scalability

Build pages with consistency:

- **Design tokens**: Define once in `globals.css`, reuse everywhere
- **Component patterns**: Establish patterns (section structure, CTA placement)
- **Naming conventions**: Consistent component and file naming
- **Shared layouts**: Use `layout.tsx` for shared UI across routes

This allows adding new pages in the same style without redefining the design system.

## Key Principles

1. **Think like a staff frontend engineer**: High-quality, production-ready code
2. **Conversion-focused**: Every design decision should support the business goal
3. **Visually stunning**: Use modern techniques (animations, gradients, effects)
4. **Brand-consistent**: Establish and maintain a cohesive design language
5. **Scalable**: Build in a way that supports adding more pages easily
