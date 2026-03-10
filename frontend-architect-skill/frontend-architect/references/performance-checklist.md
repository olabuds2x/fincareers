# Performance & SEO Checklist

## Table of Contents
1. [Core Web Vitals Targets](#core-web-vitals)
2. [Image Optimization](#images)
3. [JavaScript Optimization](#javascript)
4. [CSS Optimization](#css)
5. [Font Optimization](#fonts)
6. [SEO Essentials](#seo)
7. [Accessibility Checklist](#accessibility)
8. [Micro-Interactions Guide](#micro-interactions)

---

## Core Web Vitals Targets {#core-web-vitals}

### The Three Metrics

| Metric | Good | Needs Work | Poor |
|--------|------|------------|------|
| **LCP** (Largest Contentful Paint) | ≤2.5s | 2.5s–4s | >4s |
| **FID** (First Input Delay) | ≤100ms | 100–300ms | >300ms |
| **CLS** (Cumulative Layout Shift) | ≤0.1 | 0.1–0.25 | >0.25 |

### LCP Optimization Checklist

- [ ] Hero image preloaded: `<link rel="preload" as="image" href="...">`
- [ ] Critical CSS inlined in `<head>`
- [ ] Server response time <200ms (TTFB)
- [ ] No render-blocking resources
- [ ] Images use modern formats (WebP, AVIF)
- [ ] CDN caching enabled

**Identify LCP element:**
```javascript
new PerformanceObserver((list) => {
  const entries = list.getEntries();
  const lastEntry = entries[entries.length - 1];
  console.log('LCP element:', lastEntry.element);
}).observe({ type: 'largest-contentful-paint', buffered: true });
```

### FID/INP Optimization Checklist

- [ ] Main thread not blocked >50ms
- [ ] Event handlers complete quickly
- [ ] Heavy computation deferred to Web Workers
- [ ] Third-party scripts loaded async
- [ ] Use `requestIdleCallback` for non-critical work

### CLS Optimization Checklist

- [ ] All images have width/height or aspect-ratio
- [ ] Fonts use `font-display: swap` with size-adjust
- [ ] No injected content above existing content
- [ ] Ads/embeds have reserved space
- [ ] Animations use `transform` (not layout properties)

**Reserve space for images:**
```tsx
// Next.js Image component handles this automatically
import Image from 'next/image';

<Image
  src="/hero.jpg"
  width={1200}
  height={600}
  alt="Hero image"
  priority // Preloads LCP image
/>

// Or use CSS aspect-ratio
<div className="aspect-video bg-gray-100">
  <img src="/hero.jpg" alt="" className="h-full w-full object-cover" />
</div>
```

---

## Image Optimization {#images}

### Format Selection

| Format | Use Case | Browser Support |
|--------|----------|-----------------|
| AVIF | Photos, complex images | Chrome, Firefox |
| WebP | Universal modern format | All modern |
| PNG | Transparency needed | All |
| SVG | Icons, logos, illustrations | All |

### Next.js Image Best Practices

```tsx
import Image from 'next/image';

// Hero image (LCP candidate) - use priority
<Image
  src="/hero.jpg"
  width={1200}
  height={600}
  alt="Descriptive alt text"
  priority
  quality={85}
  placeholder="blur"
  blurDataURL="data:image/jpeg;base64,..."
/>

// Below-fold images - lazy load (default)
<Image
  src="/feature.jpg"
  width={600}
  height={400}
  alt="Feature description"
  loading="lazy"
/>
```

### Responsive Images Pattern

```tsx
// Next.js handles this with sizes prop
<Image
  src="/product.jpg"
  width={800}
  height={600}
  alt="Product"
  sizes="(max-width: 768px) 100vw, (max-width: 1200px) 50vw, 33vw"
/>

// Manual srcset for non-Next.js
<picture>
  <source
    type="image/avif"
    srcSet="/image-400.avif 400w, /image-800.avif 800w, /image-1200.avif 1200w"
    sizes="(max-width: 768px) 100vw, 50vw"
  />
  <source
    type="image/webp"
    srcSet="/image-400.webp 400w, /image-800.webp 800w, /image-1200.webp 1200w"
    sizes="(max-width: 768px) 100vw, 50vw"
  />
  <img
    src="/image-800.jpg"
    alt="Description"
    width={800}
    height={600}
    loading="lazy"
  />
</picture>
```

### Image Sizing Guidelines

| Context | Max Width | Quality |
|---------|-----------|---------|
| Hero/full-width | 1920px | 80-85 |
| Content images | 1200px | 80-85 |
| Thumbnails | 400px | 75-80 |
| Avatars | 200px | 80 |

---

## JavaScript Optimization {#javascript}

### Bundle Size Targets

| Metric | Target | Critical |
|--------|--------|----------|
| Initial JS | <100KB | <200KB |
| Total JS | <300KB | <500KB |
| Per-route JS | <50KB | <100KB |

### Code Splitting Patterns

```tsx
// Route-based splitting (automatic in Next.js App Router)
// Each page.tsx is its own chunk

// Component-level splitting
import dynamic from 'next/dynamic';

const HeavyChart = dynamic(() => import('./HeavyChart'), {
  loading: () => <div className="h-64 animate-pulse bg-gray-100" />,
  ssr: false, // Skip SSR for client-only components
});

// Conditional loading
const AdminPanel = dynamic(() => import('./AdminPanel'), {
  loading: () => <Skeleton />,
});

function Dashboard({ isAdmin }) {
  return (
    <div>
      <MainContent />
      {isAdmin && <AdminPanel />}
    </div>
  );
}
```

### Third-Party Script Loading

```tsx
// Next.js Script component
import Script from 'next/script';

// Analytics - load after page interactive
<Script
  src="https://analytics.example.com/script.js"
  strategy="afterInteractive"
/>

// Non-critical - load when idle
<Script
  src="https://widget.example.com/embed.js"
  strategy="lazyOnload"
/>

// Critical - load immediately (rare)
<Script
  src="https://critical.example.com/polyfill.js"
  strategy="beforeInteractive"
/>
```

### Tree Shaking Tips

```typescript
// BAD: Imports entire library
import _ from 'lodash';
const result = _.debounce(fn, 300);

// GOOD: Import only what you need
import debounce from 'lodash/debounce';
const result = debounce(fn, 300);

// BETTER: Use native or smaller alternatives
function debounce(fn: Function, ms: number) {
  let timeoutId: ReturnType<typeof setTimeout>;
  return (...args: any[]) => {
    clearTimeout(timeoutId);
    timeoutId = setTimeout(() => fn(...args), ms);
  };
}
```

---

## CSS Optimization {#css}

### Critical CSS Extraction

```tsx
// Next.js App Router handles this automatically
// CSS modules and Tailwind are automatically optimized

// For manual critical CSS:
<head>
  <style dangerouslySetInnerHTML={{
    __html: `
      /* Only above-fold critical styles */
      .hero { ... }
      .nav { ... }
    `
  }} />
  <link rel="preload" href="/styles.css" as="style" />
  <link rel="stylesheet" href="/styles.css" media="print" onLoad="this.media='all'" />
</head>
```

### Tailwind Production Optimization

```javascript
// tailwind.config.js
module.exports = {
  content: [
    './app/**/*.{js,ts,jsx,tsx,mdx}',
    './components/**/*.{js,ts,jsx,tsx,mdx}',
  ],
  // Purges unused CSS automatically in production
};
```

### Animation Performance

```css
/* GOOD: GPU-accelerated properties */
.animate-good {
  transform: translateX(100px);
  opacity: 0.5;
}

/* BAD: Triggers layout/paint */
.animate-bad {
  left: 100px;
  width: 200px;
  height: 200px;
}

/* Use will-change sparingly */
.will-animate {
  will-change: transform;
}
```

---

## Font Optimization {#fonts}

### Font Loading Strategy

```tsx
// Next.js font optimization
import { Inter } from 'next/font/google';

const inter = Inter({
  subsets: ['latin'],
  display: 'swap',
  variable: '--font-inter',
});

export default function RootLayout({ children }) {
  return (
    <html lang="en" className={inter.variable}>
      <body className="font-sans">{children}</body>
    </html>
  );
}
```

### Self-Hosted Fonts

```css
/* Preload critical fonts */
<link
  rel="preload"
  href="/fonts/inter-var.woff2"
  as="font"
  type="font/woff2"
  crossOrigin="anonymous"
/>

/* Font-face with fallback metrics */
@font-face {
  font-family: 'Inter';
  src: url('/fonts/inter-var.woff2') format('woff2');
  font-weight: 100 900;
  font-display: swap;
  /* Size-adjust reduces CLS from font swap */
  size-adjust: 100%;
  ascent-override: 90%;
  descent-override: 20%;
}
```

### System Font Stack (Zero Load Time)

```css
/* Maximum performance - no font loading */
body {
  font-family: 
    -apple-system, 
    BlinkMacSystemFont, 
    'Segoe UI', 
    Roboto, 
    Oxygen, 
    Ubuntu, 
    Cantarell, 
    'Fira Sans', 
    'Droid Sans', 
    'Helvetica Neue', 
    sans-serif;
}
```

---

## SEO Essentials {#seo}

### Meta Tags Template

```tsx
// app/layout.tsx
import { Metadata } from 'next';

export const metadata: Metadata = {
  title: {
    default: 'Acme - Build faster',
    template: '%s | Acme',
  },
  description: 'The modern platform for ambitious teams.',
  keywords: ['saas', 'platform', 'productivity'],
  authors: [{ name: 'Acme Inc' }],
  openGraph: {
    type: 'website',
    locale: 'en_US',
    url: 'https://acme.com',
    siteName: 'Acme',
    images: [
      {
        url: 'https://acme.com/og-image.jpg',
        width: 1200,
        height: 630,
        alt: 'Acme - Build faster',
      },
    ],
  },
  twitter: {
    card: 'summary_large_image',
    creator: '@acme',
  },
  robots: {
    index: true,
    follow: true,
  },
};
```

### Structured Data (JSON-LD)

```tsx
// components/JsonLd.tsx
export function OrganizationJsonLd() {
  const data = {
    '@context': 'https://schema.org',
    '@type': 'Organization',
    name: 'Acme Inc',
    url: 'https://acme.com',
    logo: 'https://acme.com/logo.png',
    sameAs: [
      'https://twitter.com/acme',
      'https://linkedin.com/company/acme',
    ],
  };

  return (
    <script
      type="application/ld+json"
      dangerouslySetInnerHTML={{ __html: JSON.stringify(data) }}
    />
  );
}

// For products/articles, add appropriate schema
export function ProductJsonLd({ product }) {
  const data = {
    '@context': 'https://schema.org',
    '@type': 'Product',
    name: product.name,
    description: product.description,
    image: product.image,
    offers: {
      '@type': 'Offer',
      price: product.price,
      priceCurrency: 'USD',
    },
  };

  return (
    <script
      type="application/ld+json"
      dangerouslySetInnerHTML={{ __html: JSON.stringify(data) }}
    />
  );
}
```

### Sitemap Generation

```typescript
// app/sitemap.ts (Next.js 13+)
import { MetadataRoute } from 'next';

export default function sitemap(): MetadataRoute.Sitemap {
  return [
    {
      url: 'https://acme.com',
      lastModified: new Date(),
      changeFrequency: 'weekly',
      priority: 1,
    },
    {
      url: 'https://acme.com/features',
      lastModified: new Date(),
      changeFrequency: 'monthly',
      priority: 0.8,
    },
    {
      url: 'https://acme.com/pricing',
      lastModified: new Date(),
      changeFrequency: 'monthly',
      priority: 0.8,
    },
  ];
}
```

---

## Accessibility Checklist {#accessibility}

### WCAG 2.1 AA Requirements

- [ ] **Color contrast**: 4.5:1 for normal text, 3:1 for large text
- [ ] **Focus visible**: All interactive elements have visible focus state
- [ ] **Keyboard navigable**: Tab order logical, no keyboard traps
- [ ] **Alt text**: All meaningful images have descriptive alt text
- [ ] **Headings**: Proper hierarchy (h1 → h2 → h3), no skipped levels
- [ ] **Labels**: All form inputs have associated labels
- [ ] **ARIA**: Landmarks defined, live regions for dynamic content
- [ ] **Motion**: Respect `prefers-reduced-motion`

### Focus States

```tsx
// Tailwind focus utilities
<button className="
  rounded-lg bg-gray-900 px-4 py-2 text-white
  focus:outline-none 
  focus-visible:ring-2 
  focus-visible:ring-gray-900 
  focus-visible:ring-offset-2
">
  Click me
</button>

// Skip to content link
<a
  href="#main-content"
  className="
    sr-only 
    focus:not-sr-only 
    focus:fixed 
    focus:left-4 
    focus:top-4 
    focus:z-50 
    focus:rounded 
    focus:bg-white 
    focus:px-4 
    focus:py-2 
    focus:shadow-lg
  "
>
  Skip to main content
</a>
```

### Reduced Motion

```css
/* Respect user preference */
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

```tsx
// React hook for reduced motion
function usePrefersReducedMotion() {
  const [prefersReducedMotion, setPrefersReducedMotion] = useState(false);

  useEffect(() => {
    const mediaQuery = window.matchMedia('(prefers-reduced-motion: reduce)');
    setPrefersReducedMotion(mediaQuery.matches);

    const handler = (e) => setPrefersReducedMotion(e.matches);
    mediaQuery.addEventListener('change', handler);
    return () => mediaQuery.removeEventListener('change', handler);
  }, []);

  return prefersReducedMotion;
}
```

---

## Micro-Interactions Guide {#micro-interactions}

### Timing Guidelines

| Interaction | Duration | Easing |
|-------------|----------|--------|
| Hover states | 150-200ms | ease-out |
| Button press | 100ms | ease-in |
| Modal open | 200-300ms | ease-out |
| Modal close | 150-200ms | ease-in |
| Page transitions | 300-400ms | ease-in-out |
| Loading spinners | 1000ms | linear |

### Easing Functions

```css
/* Standard easings */
--ease-out: cubic-bezier(0, 0, 0.2, 1);      /* Decelerate */
--ease-in: cubic-bezier(0.4, 0, 1, 1);       /* Accelerate */
--ease-in-out: cubic-bezier(0.4, 0, 0.2, 1); /* Smooth */

/* Premium feel */
--ease-spring: cubic-bezier(0.34, 1.56, 0.64, 1); /* Bouncy */
--ease-smooth: cubic-bezier(0.45, 0, 0.55, 1);    /* Apple-like */
```

### Button Micro-Interactions

```tsx
// Tailwind button with micro-interactions
<button className="
  rounded-lg bg-gray-900 px-6 py-3 text-white
  transition-all duration-200 ease-out
  hover:bg-gray-700 hover:shadow-md hover:-translate-y-0.5
  active:translate-y-0 active:shadow-sm
  focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-gray-900 focus-visible:ring-offset-2
">
  Get started
</button>
```

### Card Hover Effect

```tsx
<div className="
  group rounded-2xl border border-gray-200 p-6
  transition-all duration-300 ease-out
  hover:border-gray-300 hover:shadow-lg hover:-translate-y-1
">
  <h3 className="font-semibold text-gray-900 transition-colors group-hover:text-blue-600">
    Card Title
  </h3>
  <p className="mt-2 text-gray-600">Card content</p>
</div>
```

### Staggered Animation on Scroll

```tsx
// Using Framer Motion
import { motion } from 'framer-motion';

const container = {
  hidden: { opacity: 0 },
  show: {
    opacity: 1,
    transition: {
      staggerChildren: 0.1,
    },
  },
};

const item = {
  hidden: { opacity: 0, y: 20 },
  show: { opacity: 1, y: 0 },
};

function FeatureGrid({ features }) {
  return (
    <motion.div
      variants={container}
      initial="hidden"
      whileInView="show"
      viewport={{ once: true, margin: '-100px' }}
      className="grid gap-8 sm:grid-cols-2 lg:grid-cols-3"
    >
      {features.map((feature) => (
        <motion.div key={feature.id} variants={item}>
          <FeatureCard {...feature} />
        </motion.div>
      ))}
    </motion.div>
  );
}
```

### Loading States

```tsx
// Skeleton loading
function Skeleton({ className }: { className?: string }) {
  return (
    <div
      className={`animate-pulse rounded bg-gray-200 ${className}`}
      aria-hidden="true"
    />
  );
}

// Button loading state
function Button({ loading, children }) {
  return (
    <button
      disabled={loading}
      className="relative rounded-lg bg-gray-900 px-6 py-3 text-white disabled:opacity-70"
    >
      {loading && (
        <span className="absolute inset-0 flex items-center justify-center">
          <svg className="h-5 w-5 animate-spin" viewBox="0 0 24 24">
            <circle
              className="opacity-25"
              cx="12"
              cy="12"
              r="10"
              stroke="currentColor"
              strokeWidth="4"
              fill="none"
            />
            <path
              className="opacity-75"
              fill="currentColor"
              d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4z"
            />
          </svg>
        </span>
      )}
      <span className={loading ? 'invisible' : ''}>{children}</span>
    </button>
  );
}
```
