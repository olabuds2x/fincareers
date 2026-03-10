# Component Patterns Library

## Table of Contents
1. [Hero Sections](#hero)
2. [Navigation](#navigation)
3. [Feature Sections](#features)
4. [Testimonials](#testimonials)
5. [Pricing](#pricing)
6. [CTA Sections](#cta)
7. [Forms](#forms)

---

## Hero Sections {#hero}

### Pattern 1: Centered Hero (Landing Pages)

**Visual hierarchy:** Headline → Subheadline → CTA → Social proof

```tsx
// components/Hero.tsx
interface HeroProps {
  headline: string;
  subheadline: string;
  ctaText: string;
  ctaHref: string;
  socialProof?: string;
}

export function Hero({ headline, subheadline, ctaText, ctaHref, socialProof }: HeroProps) {
  return (
    <section className="relative overflow-hidden bg-white">
      {/* Subtle gradient background */}
      <div className="absolute inset-0 bg-gradient-to-b from-gray-50 to-white" />
      
      <div className="relative mx-auto max-w-7xl px-6 py-24 sm:py-32 lg:px-8 lg:py-40">
        <div className="mx-auto max-w-2xl text-center">
          {/* Headline: Display size, tight tracking */}
          <h1 className="text-4xl font-semibold tracking-tight text-gray-900 sm:text-5xl lg:text-6xl">
            {headline}
          </h1>
          
          {/* Subheadline: Muted, comfortable line height */}
          <p className="mt-6 text-lg leading-8 text-gray-600 sm:text-xl">
            {subheadline}
          </p>
          
          {/* CTA: Primary action, generous padding */}
          <div className="mt-10 flex items-center justify-center gap-x-6">
            <a
              href={ctaHref}
              className="rounded-full bg-gray-900 px-8 py-4 text-sm font-semibold text-white shadow-sm transition-all duration-200 hover:bg-gray-700 hover:shadow-md focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-gray-900"
            >
              {ctaText}
            </a>
          </div>
          
          {/* Social proof: Small, muted, trust-building */}
          {socialProof && (
            <p className="mt-8 text-sm text-gray-500">
              {socialProof}
            </p>
          )}
        </div>
      </div>
    </section>
  );
}
```

**Usage:**
```tsx
<Hero
  headline="Build faster, ship sooner"
  subheadline="The modern framework for ambitious teams. Ship production-ready code in days, not months."
  ctaText="Start for free"
  ctaHref="/signup"
  socialProof="Trusted by 10,000+ developers worldwide"
/>
```

### Pattern 2: Split Hero (SaaS/Product)

```tsx
// components/SplitHero.tsx
export function SplitHero() {
  return (
    <section className="relative overflow-hidden bg-white">
      <div className="mx-auto max-w-7xl px-6 py-24 lg:px-8 lg:py-32">
        <div className="grid gap-16 lg:grid-cols-2 lg:gap-24 items-center">
          {/* Content */}
          <div>
            <div className="inline-flex items-center rounded-full bg-gray-100 px-3 py-1 text-sm text-gray-600">
              <span className="mr-2 h-2 w-2 rounded-full bg-green-500" />
              Now in public beta
            </div>
            
            <h1 className="mt-6 text-4xl font-semibold tracking-tight text-gray-900 sm:text-5xl">
              Analytics that <span className="text-blue-600">actually help</span>
            </h1>
            
            <p className="mt-6 text-lg leading-8 text-gray-600">
              Stop drowning in data. Get actionable insights that drive growth, 
              delivered in a dashboard your team will actually use.
            </p>
            
            <div className="mt-10 flex flex-wrap gap-4">
              <a
                href="/signup"
                className="rounded-full bg-gray-900 px-6 py-3 text-sm font-semibold text-white transition-colors hover:bg-gray-700"
              >
                Get started free
              </a>
              <a
                href="/demo"
                className="rounded-full border border-gray-300 px-6 py-3 text-sm font-semibold text-gray-700 transition-colors hover:bg-gray-50"
              >
                Watch demo
              </a>
            </div>
          </div>
          
          {/* Visual */}
          <div className="relative">
            <div className="aspect-[4/3] overflow-hidden rounded-2xl bg-gray-100 shadow-2xl">
              <img
                src="/dashboard-preview.png"
                alt="Dashboard preview"
                className="h-full w-full object-cover"
              />
            </div>
            {/* Floating accent */}
            <div className="absolute -bottom-4 -left-4 rounded-xl bg-white p-4 shadow-lg">
              <div className="flex items-center gap-3">
                <div className="flex h-10 w-10 items-center justify-center rounded-full bg-green-100">
                  <svg className="h-5 w-5 text-green-600" fill="currentColor" viewBox="0 0 20 20">
                    <path fillRule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clipRule="evenodd" />
                  </svg>
                </div>
                <div>
                  <p className="text-sm font-medium text-gray-900">Revenue up 23%</p>
                  <p className="text-xs text-gray-500">vs last month</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  );
}
```

---

## Navigation {#navigation}

### Pattern: Minimal Sticky Nav

```tsx
// components/Navbar.tsx
'use client';

import { useState, useEffect } from 'react';
import Link from 'next/link';

const navLinks = [
  { href: '/features', label: 'Features' },
  { href: '/pricing', label: 'Pricing' },
  { href: '/docs', label: 'Docs' },
];

export function Navbar() {
  const [scrolled, setScrolled] = useState(false);
  const [mobileOpen, setMobileOpen] = useState(false);

  useEffect(() => {
    const handleScroll = () => setScrolled(window.scrollY > 10);
    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  }, []);

  return (
    <header
      className={`fixed top-0 z-50 w-full transition-all duration-300 ${
        scrolled 
          ? 'bg-white/80 backdrop-blur-md shadow-sm' 
          : 'bg-transparent'
      }`}
    >
      <nav className="mx-auto flex max-w-7xl items-center justify-between px-6 py-4 lg:px-8">
        {/* Logo */}
        <Link href="/" className="flex items-center gap-2">
          <div className="h-8 w-8 rounded-lg bg-gray-900" />
          <span className="text-lg font-semibold text-gray-900">Acme</span>
        </Link>

        {/* Desktop nav */}
        <div className="hidden items-center gap-8 md:flex">
          {navLinks.map((link) => (
            <Link
              key={link.href}
              href={link.href}
              className="text-sm font-medium text-gray-600 transition-colors hover:text-gray-900"
            >
              {link.label}
            </Link>
          ))}
        </div>

        {/* CTA */}
        <div className="hidden md:flex items-center gap-4">
          <Link
            href="/login"
            className="text-sm font-medium text-gray-600 transition-colors hover:text-gray-900"
          >
            Log in
          </Link>
          <Link
            href="/signup"
            className="rounded-full bg-gray-900 px-4 py-2 text-sm font-medium text-white transition-colors hover:bg-gray-700"
          >
            Get started
          </Link>
        </div>

        {/* Mobile menu button */}
        <button
          onClick={() => setMobileOpen(!mobileOpen)}
          className="md:hidden p-2 text-gray-600"
          aria-label="Toggle menu"
        >
          <svg className="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            {mobileOpen ? (
              <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M6 18L18 6M6 6l12 12" />
            ) : (
              <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M4 6h16M4 12h16M4 18h16" />
            )}
          </svg>
        </button>
      </nav>

      {/* Mobile menu */}
      {mobileOpen && (
        <div className="md:hidden bg-white border-t px-6 py-4">
          {navLinks.map((link) => (
            <Link
              key={link.href}
              href={link.href}
              className="block py-3 text-base font-medium text-gray-600"
              onClick={() => setMobileOpen(false)}
            >
              {link.label}
            </Link>
          ))}
          <div className="mt-4 pt-4 border-t">
            <Link
              href="/signup"
              className="block w-full rounded-full bg-gray-900 px-4 py-3 text-center text-sm font-medium text-white"
            >
              Get started
            </Link>
          </div>
        </div>
      )}
    </header>
  );
}
```

---

## Feature Sections {#features}

### Pattern: Feature Grid with Icons

```tsx
// components/Features.tsx
const features = [
  {
    icon: '⚡',
    title: 'Lightning fast',
    description: 'Built on edge infrastructure for sub-100ms response times globally.',
  },
  {
    icon: '🔒',
    title: 'Secure by default',
    description: 'Enterprise-grade security with SOC 2 compliance and end-to-end encryption.',
  },
  {
    icon: '📊',
    title: 'Real-time analytics',
    description: 'Track every metric that matters with our intuitive dashboard.',
  },
  {
    icon: '🔌',
    title: 'Easy integrations',
    description: 'Connect with 100+ tools your team already uses.',
  },
];

export function Features() {
  return (
    <section className="bg-white py-24 sm:py-32">
      <div className="mx-auto max-w-7xl px-6 lg:px-8">
        {/* Section header */}
        <div className="mx-auto max-w-2xl text-center">
          <p className="text-sm font-semibold uppercase tracking-wide text-blue-600">
            Features
          </p>
          <h2 className="mt-2 text-3xl font-semibold tracking-tight text-gray-900 sm:text-4xl">
            Everything you need to scale
          </h2>
          <p className="mt-4 text-lg text-gray-600">
            Powerful features designed to help your team move faster.
          </p>
        </div>

        {/* Feature grid */}
        <div className="mt-16 grid gap-8 sm:grid-cols-2 lg:grid-cols-4">
          {features.map((feature, index) => (
            <div
              key={feature.title}
              className="group relative rounded-2xl border border-gray-200 p-8 transition-all duration-200 hover:border-gray-300 hover:shadow-lg"
            >
              {/* Icon */}
              <div className="mb-4 text-4xl">{feature.icon}</div>
              
              {/* Title */}
              <h3 className="text-lg font-semibold text-gray-900">
                {feature.title}
              </h3>
              
              {/* Description */}
              <p className="mt-2 text-sm leading-6 text-gray-600">
                {feature.description}
              </p>
            </div>
          ))}
        </div>
      </div>
    </section>
  );
}
```

---

## Testimonials {#testimonials}

### Pattern: Single Featured Testimonial

```tsx
// components/Testimonial.tsx
export function Testimonial() {
  return (
    <section className="bg-gray-50 py-24 sm:py-32">
      <div className="mx-auto max-w-7xl px-6 lg:px-8">
        <figure className="mx-auto max-w-2xl">
          {/* Quote */}
          <blockquote className="text-center text-xl font-medium leading-8 text-gray-900 sm:text-2xl sm:leading-9">
            <p>
              "This tool has completely transformed how our team works. We've cut our 
              deployment time by 80% and haven't looked back."
            </p>
          </blockquote>
          
          {/* Attribution */}
          <figcaption className="mt-10 flex items-center justify-center gap-x-4">
            <img
              src="/testimonial-avatar.jpg"
              alt=""
              className="h-12 w-12 rounded-full bg-gray-100 object-cover"
            />
            <div className="text-left">
              <p className="font-semibold text-gray-900">Sarah Chen</p>
              <p className="text-sm text-gray-600">CTO at TechCorp</p>
            </div>
          </figcaption>
        </figure>
      </div>
    </section>
  );
}
```

---

## Pricing {#pricing}

### Pattern: Three-Tier Pricing

```tsx
// components/Pricing.tsx
const tiers = [
  {
    name: 'Starter',
    price: '$0',
    description: 'Perfect for trying out our platform.',
    features: ['Up to 1,000 events/mo', 'Basic analytics', 'Email support'],
    cta: 'Start free',
    highlighted: false,
  },
  {
    name: 'Pro',
    price: '$29',
    description: 'Everything you need to grow.',
    features: ['Unlimited events', 'Advanced analytics', 'Priority support', 'Custom integrations'],
    cta: 'Start trial',
    highlighted: true,
  },
  {
    name: 'Enterprise',
    price: 'Custom',
    description: 'For large-scale operations.',
    features: ['Everything in Pro', 'Dedicated support', 'SLA guarantee', 'Custom contracts'],
    cta: 'Contact sales',
    highlighted: false,
  },
];

export function Pricing() {
  return (
    <section className="bg-white py-24 sm:py-32">
      <div className="mx-auto max-w-7xl px-6 lg:px-8">
        {/* Header */}
        <div className="mx-auto max-w-2xl text-center">
          <h2 className="text-3xl font-semibold tracking-tight text-gray-900 sm:text-4xl">
            Simple, transparent pricing
          </h2>
          <p className="mt-4 text-lg text-gray-600">
            Choose the plan that fits your needs. Upgrade anytime.
          </p>
        </div>

        {/* Pricing cards */}
        <div className="mt-16 grid gap-8 lg:grid-cols-3">
          {tiers.map((tier) => (
            <div
              key={tier.name}
              className={`relative rounded-2xl p-8 ${
                tier.highlighted
                  ? 'bg-gray-900 text-white ring-2 ring-gray-900'
                  : 'bg-white ring-1 ring-gray-200'
              }`}
            >
              {tier.highlighted && (
                <span className="absolute -top-4 left-1/2 -translate-x-1/2 rounded-full bg-blue-600 px-4 py-1 text-xs font-semibold text-white">
                  Most popular
                </span>
              )}
              
              <h3 className={`text-lg font-semibold ${tier.highlighted ? 'text-white' : 'text-gray-900'}`}>
                {tier.name}
              </h3>
              
              <p className={`mt-4 flex items-baseline gap-x-1 ${tier.highlighted ? 'text-white' : 'text-gray-900'}`}>
                <span className="text-4xl font-bold">{tier.price}</span>
                {tier.price !== 'Custom' && <span className="text-sm text-gray-500">/month</span>}
              </p>
              
              <p className={`mt-4 text-sm ${tier.highlighted ? 'text-gray-300' : 'text-gray-600'}`}>
                {tier.description}
              </p>
              
              <ul className="mt-8 space-y-3">
                {tier.features.map((feature) => (
                  <li key={feature} className="flex items-center gap-3 text-sm">
                    <svg className={`h-5 w-5 flex-shrink-0 ${tier.highlighted ? 'text-blue-400' : 'text-blue-600'}`} fill="currentColor" viewBox="0 0 20 20">
                      <path fillRule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clipRule="evenodd" />
                    </svg>
                    <span className={tier.highlighted ? 'text-gray-300' : 'text-gray-600'}>
                      {feature}
                    </span>
                  </li>
                ))}
              </ul>
              
              <a
                href="#"
                className={`mt-8 block rounded-full px-4 py-3 text-center text-sm font-semibold transition-colors ${
                  tier.highlighted
                    ? 'bg-white text-gray-900 hover:bg-gray-100'
                    : 'bg-gray-900 text-white hover:bg-gray-700'
                }`}
              >
                {tier.cta}
              </a>
            </div>
          ))}
        </div>
      </div>
    </section>
  );
}
```

---

## CTA Sections {#cta}

### Pattern: Final CTA with Gradient

```tsx
// components/FinalCTA.tsx
export function FinalCTA() {
  return (
    <section className="relative overflow-hidden bg-gray-900 py-24 sm:py-32">
      {/* Background gradient */}
      <div className="absolute inset-0 bg-gradient-to-br from-gray-900 via-gray-800 to-gray-900" />
      <div className="absolute inset-0 bg-[url('/grid.svg')] opacity-10" />
      
      <div className="relative mx-auto max-w-7xl px-6 lg:px-8">
        <div className="mx-auto max-w-2xl text-center">
          <h2 className="text-3xl font-semibold tracking-tight text-white sm:text-4xl">
            Ready to get started?
          </h2>
          <p className="mt-4 text-lg text-gray-300">
            Join thousands of teams already building better products.
          </p>
          <div className="mt-10 flex flex-wrap items-center justify-center gap-4">
            <a
              href="/signup"
              className="rounded-full bg-white px-8 py-4 text-sm font-semibold text-gray-900 transition-all hover:bg-gray-100"
            >
              Start your free trial
            </a>
            <a
              href="/contact"
              className="rounded-full border border-gray-600 px-8 py-4 text-sm font-semibold text-white transition-all hover:border-gray-500 hover:bg-gray-800"
            >
              Talk to sales
            </a>
          </div>
        </div>
      </div>
    </section>
  );
}
```

---

## Forms {#forms}

### Pattern: Minimal Input with Floating Label

```tsx
// components/Input.tsx
'use client';

import { useState } from 'react';

interface InputProps {
  label: string;
  type?: string;
  name: string;
  required?: boolean;
}

export function Input({ label, type = 'text', name, required }: InputProps) {
  const [focused, setFocused] = useState(false);
  const [value, setValue] = useState('');

  const isActive = focused || value;

  return (
    <div className="relative">
      <input
        type={type}
        name={name}
        id={name}
        required={required}
        value={value}
        onChange={(e) => setValue(e.target.value)}
        onFocus={() => setFocused(true)}
        onBlur={() => setFocused(false)}
        className="peer w-full rounded-lg border border-gray-300 bg-transparent px-4 pb-2 pt-6 text-base text-gray-900 outline-none transition-all focus:border-gray-900 focus:ring-1 focus:ring-gray-900"
      />
      <label
        htmlFor={name}
        className={`absolute left-4 transition-all duration-200 ${
          isActive
            ? 'top-2 text-xs text-gray-500'
            : 'top-4 text-base text-gray-400'
        }`}
      >
        {label}
      </label>
    </div>
  );
}
```
