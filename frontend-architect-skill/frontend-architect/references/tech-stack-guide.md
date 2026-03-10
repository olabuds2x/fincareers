# Tech Stack Selection Guide

## Table of Contents
1. [Framework Decision Matrix](#framework-matrix)
2. [Stack by Project Type](#stack-by-type)
3. [Styling Approaches](#styling)
4. [State Management](#state)
5. [Deployment & Hosting](#deployment)

---

## Framework Decision Matrix {#framework-matrix}

### Quick Selection Guide

| Project Type | Interactivity | Content Updates | Recommended |
|--------------|---------------|-----------------|-------------|
| Landing page | Low | Rare | Astro |
| Marketing site | Low-Medium | Weekly | Astro or Next.js (SSG) |
| Blog/Content | Low | Daily | Astro or Next.js (SSG) |
| SaaS Dashboard | High | Real-time | Next.js App Router |
| E-commerce (small) | Medium | Daily | Next.js (ISR) |
| E-commerce (large) | High | Real-time | Next.js + Edge |
| Web App | High | Real-time | Next.js or Remix |

### Framework Deep Dive

#### Astro
**Best for:** Content-heavy sites, landing pages, blogs

**Why choose:**
- Zero JS by default (ships HTML)
- Island architecture for selective hydration
- Fastest time-to-first-byte
- MDX support built-in

**When NOT to use:**
- Heavy client-side interactivity
- Real-time data requirements
- Complex authentication flows

```bash
# Quick start
npm create astro@latest
```

#### Next.js (App Router)
**Best for:** Full-stack applications, SaaS, e-commerce

**Why choose:**
- React Server Components
- Streaming and Suspense
- Built-in API routes
- ISR for hybrid static/dynamic
- Edge runtime support

**Key decisions:**
```
/app directory structure:
├── (marketing)/     # Route group for landing pages
│   ├── page.tsx     # Static, no client JS
│   └── layout.tsx   # Shared marketing layout
├── (dashboard)/     # Route group for app
│   ├── page.tsx     # Dynamic, authenticated
│   └── layout.tsx   # App shell with nav
└── api/             # API routes
```

#### Remix
**Best for:** Form-heavy apps, progressive enhancement focus

**Why choose:**
- Nested routing with data loading
- Progressive enhancement by default
- Better error boundaries
- Form handling built-in

**When NOT to use:**
- Static content sites
- When ISR is needed

### Rendering Strategy Matrix

| Strategy | Use Case | Next.js | Astro |
|----------|----------|---------|-------|
| SSG | Static content | `generateStaticParams` | Default |
| SSR | Personalized content | `dynamic = 'force-dynamic'` | `export const prerender = false` |
| ISR | Frequent updates | `revalidate: 60` | N/A |
| CSR | Highly interactive | `'use client'` | `client:load` |

---

## Stack by Project Type {#stack-by-type}

### Landing Page Stack

```
Framework: Astro
Styling: Tailwind CSS
Animations: CSS + View Transitions API
Forms: Astro Actions or Formspree
Analytics: Plausible or Fathom
Hosting: Vercel or Netlify

Dependencies:
- astro
- @astrojs/tailwind
- @astrojs/sitemap
```

**Project structure:**
```
/src
├── components/
│   ├── Hero.astro
│   ├── Features.astro
│   ├── Testimonials.astro
│   ├── Pricing.astro
│   └── CTA.astro
├── layouts/
│   └── Base.astro
└── pages/
    └── index.astro
```

### SaaS Dashboard Stack

```
Framework: Next.js 14+ (App Router)
Styling: Tailwind CSS + shadcn/ui
State: Zustand or Jotai
Auth: NextAuth.js or Clerk
Database: Prisma + PostgreSQL
API: tRPC or Server Actions
Hosting: Vercel

Dependencies:
- next
- react
- tailwindcss
- @shadcn/ui
- zustand
- next-auth
- prisma
- @trpc/client (optional)
```

**Project structure:**
```
/app
├── (auth)/
│   ├── login/page.tsx
│   └── register/page.tsx
├── (dashboard)/
│   ├── layout.tsx        # Sidebar + header
│   ├── page.tsx          # Dashboard home
│   ├── settings/page.tsx
│   └── [feature]/page.tsx
├── api/
│   └── trpc/[trpc]/route.ts
└── layout.tsx            # Root layout
/components
├── ui/                   # shadcn components
├── dashboard/            # Dashboard-specific
└── shared/               # Shared components
```

### E-commerce Stack

```
Framework: Next.js 14+ (App Router)
Styling: Tailwind CSS
Commerce: Shopify Storefront API or Medusa
Payments: Stripe
Search: Algolia or Typesense
CDN: Cloudflare Images
Hosting: Vercel (Edge)

Dependencies:
- next
- react
- tailwindcss
- @shopify/hydrogen-react (or medusa-react)
- stripe
- algoliasearch
```

**Key patterns:**
```typescript
// ISR for product pages
export const revalidate = 60; // Revalidate every 60s

// Edge runtime for cart
export const runtime = 'edge';

// Streaming for product grid
import { Suspense } from 'react';
<Suspense fallback={<ProductSkeleton />}>
  <ProductGrid />
</Suspense>
```

---

## Styling Approaches {#styling}

### Tailwind CSS (Recommended)

**Why Tailwind:**
- Utility-first = consistent spacing/colors
- Purged CSS = tiny bundles
- Design system built-in
- Co-located with components

**Configuration:**
```javascript
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      fontFamily: {
        sans: ['Inter', ...defaultTheme.fontFamily.sans],
      },
      spacing: {
        '18': '4.5rem',
        '88': '22rem',
      },
      animation: {
        'fade-in': 'fadeIn 0.5s ease-out',
        'slide-up': 'slideUp 0.5s ease-out',
      },
      keyframes: {
        fadeIn: {
          '0%': { opacity: '0' },
          '100%': { opacity: '1' },
        },
        slideUp: {
          '0%': { opacity: '0', transform: 'translateY(10px)' },
          '100%': { opacity: '1', transform: 'translateY(0)' },
        },
      },
    },
  },
  plugins: [
    require('@tailwindcss/typography'),
    require('@tailwindcss/forms'),
  ],
};
```

### Component Library: shadcn/ui

**Why shadcn:**
- Copy-paste, not dependency
- Full control over code
- Accessible by default (Radix primitives)
- Tailwind-native

**Installation:**
```bash
npx shadcn-ui@latest init
npx shadcn-ui@latest add button card dialog
```

### CSS Custom Properties for Theming

```css
:root {
  --color-primary: 220 90% 56%;
  --color-background: 0 0% 100%;
  --color-foreground: 222 47% 11%;
  --radius: 0.5rem;
}

.dark {
  --color-background: 222 47% 11%;
  --color-foreground: 210 40% 98%;
}
```

---

## State Management {#state}

### Selection Guide

| Complexity | Scope | Recommendation |
|------------|-------|----------------|
| Simple | Component | useState/useReducer |
| Medium | Feature | Zustand |
| Complex | Global | Zustand + React Query |
| Server-heavy | Full app | React Query alone |

### Zustand Pattern

```typescript
// stores/app-store.ts
import { create } from 'zustand';
import { persist } from 'zustand/middleware';

interface AppState {
  sidebarOpen: boolean;
  theme: 'light' | 'dark' | 'system';
  toggleSidebar: () => void;
  setTheme: (theme: AppState['theme']) => void;
}

export const useAppStore = create<AppState>()(
  persist(
    (set) => ({
      sidebarOpen: true,
      theme: 'system',
      toggleSidebar: () => set((s) => ({ sidebarOpen: !s.sidebarOpen })),
      setTheme: (theme) => set({ theme }),
    }),
    { name: 'app-storage' }
  )
);
```

### React Query for Server State

```typescript
// hooks/use-products.ts
import { useQuery, useMutation, useQueryClient } from '@tanstack/react-query';

export function useProducts() {
  return useQuery({
    queryKey: ['products'],
    queryFn: fetchProducts,
    staleTime: 1000 * 60 * 5, // 5 minutes
  });
}

export function useCreateProduct() {
  const queryClient = useQueryClient();
  
  return useMutation({
    mutationFn: createProduct,
    onSuccess: () => {
      queryClient.invalidateQueries({ queryKey: ['products'] });
    },
  });
}
```

---

## Deployment & Hosting {#deployment}

### Platform Comparison

| Platform | Best For | Edge Support | Pricing Model |
|----------|----------|--------------|---------------|
| Vercel | Next.js, Astro | Yes | Per-request |
| Netlify | Static, Astro | Yes | Per-site bandwidth |
| Cloudflare Pages | Static, Workers | Yes | Generous free tier |
| Railway | Full-stack, DB | No | Per-resource |

### Vercel Configuration

```json
// vercel.json
{
  "headers": [
    {
      "source": "/(.*)",
      "headers": [
        { "key": "X-Content-Type-Options", "value": "nosniff" },
        { "key": "X-Frame-Options", "value": "DENY" },
        { "key": "X-XSS-Protection", "value": "1; mode=block" }
      ]
    },
    {
      "source": "/fonts/(.*)",
      "headers": [
        { "key": "Cache-Control", "value": "public, max-age=31536000, immutable" }
      ]
    }
  ]
}
```

### Environment Variables Pattern

```bash
# .env.local (development)
NEXT_PUBLIC_API_URL=http://localhost:3000/api
DATABASE_URL=postgresql://...

# .env.production (production)
NEXT_PUBLIC_API_URL=https://api.example.com
DATABASE_URL=postgresql://...
```

**Security rule:** Never prefix secrets with `NEXT_PUBLIC_` — they'll be exposed to the browser.
