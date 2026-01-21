# AquaShine Pool Services - Complete Website PRD (2026 Edition)

## OVERVIEW

Build a complete, production-ready pool services website for AquaShine Pool Services using cutting-edge 2026 web technologies. The website must support both subscription-based recurring payments and one-time payments through Stripe Checkout. The site should be professional, mobile-first, blazing fast, and conversion-optimized.

**This is a COMPLETE specification. Implement EVERYTHING described below without asking questions.**

**Updated**: January 2026 with Next.js 16, React 19.2, Tailwind v4, and latest best practices

---

## BUSINESS INFORMATION

```
Business Name: AquaShine Pool Services
Phone: 917-340-6578
Email: info@aquashinepools.com
Service Area: Orlando, Kissimmee, and surrounding Central Florida communities
Counties Served: Orange County, Osceola County, Seminole County
Tagline: "Crystal Clear Pools, Zero Hassle"
Year Established: 2024
```

---

## TECH STACK (2026 MODERN STACK)

```
Framework: Next.js 16.1 (App Router, Turbopack)
Runtime: Node.js 22 LTS
Language: TypeScript 5.9+ (strict mode)
Styling: Tailwind CSS v4.0
Payments: Stripe Checkout (API v2025-12-15)
UI Library: React 19.2
Icons: Lucide React (latest)
Form Handling: React Hook Form v7+ with Zod v3.23+
Font: Geist Sans (Vercel's optimized font) + Inter fallback
State Management: React 19 useOptimistic + Server Actions
Bundler: Turbopack (default in Next.js 16)
```

### Package.json Dependencies (2026)

```json
{
  "name": "aquashine-pool-services",
  "version": "1.0.0",
  "private": true,
  "scripts": {
    "dev": "next dev --turbopack",
    "build": "next build",
    "start": "next start",
    "lint": "next lint",
    "type-check": "tsc --noEmit"
  },
  "dependencies": {
    "next": "^16.1.0",
    "react": "^19.2.0",
    "react-dom": "^19.2.0",
    "stripe": "^17.5.0",
    "@stripe/stripe-js": "^4.13.0",
    "lucide-react": "^0.460.0",
    "react-hook-form": "^7.54.0",
    "@hookform/resolvers": "^3.9.1",
    "zod": "^3.23.8",
    "clsx": "^2.1.1",
    "tailwind-merge": "^2.6.0",
    "geist": "^1.3.1"
  },
  "devDependencies": {
    "@types/node": "^22.10.2",
    "@types/react": "^19.0.1",
    "@types/react-dom": "^19.0.2",
    "typescript": "^5.9.3",
    "tailwindcss": "^4.0.0",
    "@tailwindcss/vite": "^4.0.0",
    "autoprefixer": "^10.4.20",
    "eslint": "^9.17.0",
    "eslint-config-next": "^16.1.0"
  },
  "engines": {
    "node": ">=22.0.0",
    "npm": ">=10.0.0"
  }
}
```

---

## DESIGN SYSTEM (Tailwind v4)

### Tailwind v4 Configuration

**New Setup (Tailwind v4):**
```css
/* src/app/globals.css */
@import "tailwindcss";

@theme {
  /* Custom color palette */
  --color-primary-50: #EBF8FF;
  --color-primary-100: #CAF0F8;
  --color-primary-200: #90E0EF;
  --color-primary-300: #00B4D8;
  --color-primary-400: #0096C7;
  --color-primary-500: #0077B6;
  --color-primary-600: #005F8A;
  --color-primary-700: #004A6E;
  --color-primary-800: #003652;
  --color-primary-900: #03045E;

  --color-accent: #03045E;
  --color-accent-light: #023E8A;

  /* Font family */
  --font-sans: 'Geist Sans', 'Inter', system-ui, -apple-system, sans-serif;
}
```

### Typography Scale (2026)

```
H1: text-4xl md:text-5xl lg:text-6xl font-bold tracking-tight
H2: text-3xl md:text-4xl font-bold tracking-tight
H3: text-2xl md:text-3xl font-semibold
H4: text-xl md:text-2xl font-semibold
Body Large: text-lg leading-relaxed
Body: text-base leading-relaxed
Small: text-sm
Caption: text-xs text-gray-500
```

### Spacing System

```
Section Padding: py-16 md:py-20 lg:py-24
Container: max-w-7xl mx-auto px-4 sm:px-6 lg:px-8
Card Padding: p-6 md:p-8
Gap (Grid): gap-6 md:gap-8
Stack Spacing: space-y-4 md:space-y-6
```

### Component Styles (Using Tailwind v4)

```css
/* Button variants - using @layer components */
@layer components {
  .btn-primary {
    @apply inline-flex items-center justify-center
           bg-primary-500 hover:bg-primary-600
           text-white font-semibold
           px-6 py-3 rounded-lg
           transition-all duration-200
           shadow-md hover:shadow-lg
           focus:outline-none focus:ring-2 focus:ring-primary-500 focus:ring-offset-2
           disabled:opacity-50 disabled:cursor-not-allowed;
  }

  .btn-secondary {
    @apply inline-flex items-center justify-center
           bg-white hover:bg-gray-50
           text-primary-600 font-semibold
           border-2 border-primary-500
           px-6 py-3 rounded-lg
           transition-all duration-200
           focus:outline-none focus:ring-2 focus:ring-primary-500 focus:ring-offset-2;
  }

  .card {
    @apply bg-white rounded-2xl shadow-lg border border-gray-100
           hover:shadow-xl transition-shadow duration-300;
  }

  .input-field {
    @apply w-full px-4 py-3 rounded-lg
           border border-gray-300
           focus:border-primary-500 focus:ring-2 focus:ring-primary-500/20
           transition-all duration-200
           placeholder:text-gray-400
           outline-none;
  }
}
```

---

## FILE STRUCTURE (Next.js 16)

```
aquashine/
├── .env.local                    # Environment variables (gitignored)
├── .env.example                  # Example env file
├── next.config.ts                # Next.js 16 config (TypeScript)
├── tsconfig.json
├── package.json
├── .eslintrc.json
├── .gitignore
├── public/
│   ├── favicon.ico
│   ├── og-image.jpg             # 1200x630 OG image
│   └── images/
│       └── pool-hero.jpg        # Hero background
├── src/
│   ├── app/
│   │   ├── layout.tsx           # Root layout with metadata
│   │   ├── page.tsx             # Home page
│   │   ├── globals.css          # Tailwind v4 + custom styles
│   │   ├── services/
│   │   │   └── page.tsx         # Services page
│   │   ├── book/
│   │   │   └── page.tsx         # Booking page
│   │   ├── contact/
│   │   │   └── page.tsx         # Contact page
│   │   ├── success/
│   │   │   └── page.tsx         # Payment success
│   │   ├── canceled/
│   │   │   └── page.tsx         # Payment canceled
│   │   └── api/
│   │       └── checkout/
│   │           └── route.ts     # Stripe checkout API (Server Action alternative)
│   ├── components/
│   │   ├── layout/
│   │   │   ├── Header.tsx
│   │   │   ├── Footer.tsx
│   │   │   ├── MobileMenu.tsx
│   │   │   └── Container.tsx
│   │   ├── home/
│   │   │   ├── Hero.tsx
│   │   │   ├── ServicesPreview.tsx
│   │   │   ├── WhyChooseUs.tsx
│   │   │   ├── Testimonials.tsx
│   │   │   └── HomeCTA.tsx
│   │   ├── services/
│   │   │   ├── ServiceCard.tsx
│   │   │   └── ServicesList.tsx
│   │   ├── booking/
│   │   │   ├── BookingCard.tsx
│   │   │   └── BookingGrid.tsx
│   │   ├── contact/
│   │   │   ├── ContactForm.tsx
│   │   │   └── ContactInfo.tsx
│   │   └── ui/
│   │       ├── Button.tsx
│   │       ├── Badge.tsx
│   │       ├── Card.tsx
│   │       └── Input.tsx
│   ├── lib/
│   │   ├── stripe.ts            # Stripe server config
│   │   ├── stripe-client.ts     # Stripe client config
│   │   └── utils.ts             # Utility functions
│   ├── data/
│   │   └── services.ts          # Services data
│   ├── types/
│   │   └── index.ts             # TypeScript types
│   └── actions/
│       └── checkout.ts          # Server Actions (alternative to API route)
```

---

## NEXT.JS 16 OPTIMIZATIONS

### Enable Turbopack (Default)
```typescript
// next.config.ts
import type { NextConfig } from 'next'

const config: NextConfig = {
  // Turbopack is now default in dev
  // No need to specify --turbopack flag

  experimental: {
    // Use cache directive for static parts
    dynamicIO: true,
  },

  images: {
    formats: ['image/avif', 'image/webp'],
    deviceSizes: [640, 768, 1024, 1280, 1536],
  },
}

export default config
```

### Use "use cache" Directive (Next.js 16)
```typescript
// Example: Cache service data
'use cache'

export async function getServices() {
  return services
}
```

---

## TYPES (src/types/index.ts)

```typescript
export interface Service {
  id: string
  name: string
  shortName: string
  price: number
  unit: 'week' | 'visit' | 'one-time'
  type: 'subscription' | 'one_time'
  interval?: 'week' | 'month'
  description: string
  shortDescription: string
  includes: string[]
  popular?: boolean
  icon: string
}

export interface Testimonial {
  id: string
  name: string
  location: string
  text: string
  rating: number
}

export interface ContactFormData {
  name: string
  email: string
  phone: string
  address?: string
  service?: string
  message: string
}

export interface CheckoutRequest {
  serviceId: string
  serviceName: string
  price: number
  type: 'subscription' | 'one_time'
  interval?: 'week' | 'month'
}

export interface NavLink {
  label: string
  href: string
}

export interface Feature {
  icon: string
  title: string
  description: string
}
```

---

## STRIPE CONFIGURATION (2026)

### lib/stripe.ts (Server)

```typescript
import Stripe from 'stripe'

if (!process.env.STRIPE_SECRET_KEY) {
  throw new Error('STRIPE_SECRET_KEY is not set in environment variables')
}

export const stripe = new Stripe(process.env.STRIPE_SECRET_KEY, {
  apiVersion: '2025-12-15',  // Latest API version
  typescript: true,
  appInfo: {
    name: 'AquaShine Pool Services',
    version: '1.0.0',
  },
})
```

### lib/stripe-client.ts (Client)

```typescript
import { loadStripe, Stripe } from '@stripe/stripe-js'

let stripePromise: Promise<Stripe | null>

export const getStripe = () => {
  if (!stripePromise) {
    const key = process.env.NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY
    if (!key) {
      throw new Error('NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY is not set')
    }
    stripePromise = loadStripe(key)
  }
  return stripePromise
}
```

### Environment Variables (.env.local)

```bash
# Stripe Keys (use test keys for development)
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_test_YOUR_KEY_HERE
STRIPE_SECRET_KEY=sk_test_YOUR_KEY_HERE

# Base URL
NEXT_PUBLIC_BASE_URL=http://localhost:3000
```

---

## API ROUTE (src/app/api/checkout/route.ts)

```typescript
import { NextRequest, NextResponse } from 'next/server'
import { stripe } from '@/lib/stripe'
import { services } from '@/data/services'

export async function POST(request: NextRequest) {
  try {
    const body = await request.json()
    const { serviceId } = body

    // Find the service
    const service = services.find((s) => s.id === serviceId)

    if (!service) {
      return NextResponse.json(
        { error: 'Service not found' },
        { status: 404 }
      )
    }

    const baseUrl = process.env.NEXT_PUBLIC_BASE_URL || 'http://localhost:3000'

    // Create checkout session based on service type
    if (service.type === 'subscription') {
      const session = await stripe.checkout.sessions.create({
        mode: 'subscription',
        payment_method_types: ['card'],
        line_items: [
          {
            price_data: {
              currency: 'usd',
              product_data: {
                name: service.name,
                description: service.shortDescription,
              },
              unit_amount: service.price * 100,
              recurring: {
                interval: service.interval === 'week' ? 'week' : 'month',
                interval_count: service.id === 'biweekly-maintenance' ? 2 : 1,
              },
            },
            quantity: 1,
          },
        ],
        success_url: `${baseUrl}/success?session_id={CHECKOUT_SESSION_ID}&service=${service.id}`,
        cancel_url: `${baseUrl}/canceled?service=${service.id}`,
        customer_creation: 'always',
        billing_address_collection: 'required',
        phone_number_collection: {
          enabled: true,
        },
        custom_fields: [
          {
            key: 'service_address',
            label: {
              type: 'custom',
              custom: 'Service Address (where is your pool?)',
            },
            type: 'text',
          },
        ],
        metadata: {
          serviceId: service.id,
          serviceName: service.name,
          serviceType: service.type,
        },
      })

      return NextResponse.json({ url: session.url })
    } else {
      const session = await stripe.checkout.sessions.create({
        mode: 'payment',
        payment_method_types: ['card'],
        line_items: [
          {
            price_data: {
              currency: 'usd',
              product_data: {
                name: service.name,
                description: service.shortDescription,
              },
              unit_amount: service.price * 100,
            },
            quantity: 1,
          },
        ],
        success_url: `${baseUrl}/success?session_id={CHECKOUT_SESSION_ID}&service=${service.id}`,
        cancel_url: `${baseUrl}/canceled?service=${service.id}`,
        customer_creation: 'always',
        billing_address_collection: 'required',
        phone_number_collection: {
          enabled: true,
        },
        custom_fields: [
          {
            key: 'service_address',
            label: {
              type: 'custom',
              custom: 'Service Address (where is your pool?)',
            },
            type: 'text',
          },
          {
            key: 'preferred_date',
            label: {
              type: 'custom',
              custom: 'Preferred Service Date',
            },
            type: 'text',
            optional: true,
          },
        ],
        metadata: {
          serviceId: service.id,
          serviceName: service.name,
          serviceType: service.type,
        },
      })

      return NextResponse.json({ url: session.url })
    }
  } catch (error) {
    console.error('Checkout error:', error)
    return NextResponse.json(
      { error: 'Failed to create checkout session' },
      { status: 500 }
    )
  }
}
```

---

## ROOT LAYOUT (src/app/layout.tsx) - 2026 VERSION

```typescript
import type { Metadata } from 'next'
import { GeistSans } from 'geist/font/sans'
import './globals.css'
import Header from '@/components/layout/Header'
import Footer from '@/components/layout/Footer'

export const metadata: Metadata = {
  title: {
    default: 'AquaShine Pool Services | Orlando & Kissimmee Pool Cleaning',
    template: '%s | AquaShine Pool Services',
  },
  description: 'Professional pool cleaning and maintenance services in Orlando, Kissimmee, and Central Florida. Weekly maintenance, one-time cleaning, and more. Call (917) 340-6578.',
  keywords: ['pool cleaning', 'pool maintenance', 'Orlando pool service', 'Kissimmee pool cleaning', 'Central Florida pool care'],
  authors: [{ name: 'AquaShine Pool Services' }],
  openGraph: {
    type: 'website',
    locale: 'en_US',
    url: 'https://aquashinepools.com',
    siteName: 'AquaShine Pool Services',
    title: 'AquaShine Pool Services | Orlando & Kissimmee Pool Cleaning',
    description: 'Professional pool cleaning and maintenance services in Orlando, Kissimmee, and Central Florida.',
    images: [
      {
        url: '/og-image.jpg',
        width: 1200,
        height: 630,
        alt: 'AquaShine Pool Services',
      },
    ],
  },
  twitter: {
    card: 'summary_large_image',
    title: 'AquaShine Pool Services',
    description: 'Professional pool cleaning in Orlando & Kissimmee',
    images: ['/og-image.jpg'],
  },
  robots: {
    index: true,
    follow: true,
  },
}

const jsonLd = {
  '@context': 'https://schema.org',
  '@type': 'LocalBusiness',
  name: 'AquaShine Pool Services',
  description: 'Professional pool cleaning and maintenance services in Orlando, Kissimmee, and Central Florida.',
  telephone: '+1-917-340-6578',
  email: 'info@aquashinepools.com',
  areaServed: ['Orlando', 'Kissimmee', 'Winter Garden', 'Winter Park', 'Lake Nona'],
  priceRange: '$$',
  address: {
    '@type': 'PostalAddress',
    addressLocality: 'Orlando',
    addressRegion: 'FL',
    addressCountry: 'US',
  },
}

export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <html lang="en" className={GeistSans.variable}>
      <body className="min-h-screen flex flex-col bg-white text-gray-900 antialiased">
        <script
          type="application/ld+json"
          dangerouslySetInnerHTML={{ __html: JSON.stringify(jsonLd) }}
        />
        <Header />
        <main className="flex-grow">{children}</main>
        <Footer />
      </body>
    </html>
  )
}
```

---

## 2026 PERFORMANCE OPTIMIZATIONS

### Use React 19.2 Features

```typescript
// Example: useOptimistic for instant UI updates
'use client'

import { useOptimistic } from 'react'

export function BookingButton({ service }) {
  const [optimisticState, addOptimistic] = useOptimistic(
    { status: 'idle' },
    (state, newStatus) => ({ ...state, status: newStatus })
  )

  async function handleBook() {
    addOptimistic('loading')
    // Redirect to Stripe...
  }

  return (
    <button disabled={optimisticState.status === 'loading'}>
      {optimisticState.status === 'loading' ? 'Processing...' : 'Book Now'}
    </button>
  )
}
```

### Streaming and Suspense

```typescript
import { Suspense } from 'react'

export default function ServicesPage() {
  return (
    <Suspense fallback={<LoadingSkeleton />}>
      <ServicesList />
    </Suspense>
  )
}
```

---

## ACCESSIBILITY (2026 WCAG 2.2 Level AA)

1. ✅ Keyboard navigation for all interactive elements
2. ✅ Proper ARIA labels and landmarks
3. ✅ Focus indicators (visible focus rings)
4. ✅ Color contrast ratio 4.5:1 minimum
5. ✅ Semantic HTML5 elements
6. ✅ Form labels and error announcements
7. ✅ Skip to main content link
8. ✅ Reduced motion support (`prefers-reduced-motion`)
9. ✅ Touch target size minimum 44x44px
10. ✅ Screen reader tested

---

## DEPLOYMENT (Vercel - 2026)

```bash
# Install Vercel CLI
npm i -g vercel@latest

# Deploy
vercel --prod

# Environment variables (set in Vercel dashboard):
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_live_...
STRIPE_SECRET_KEY=sk_live_...
NEXT_PUBLIC_BASE_URL=https://aquashinepools.com
```

### Vercel Configuration (vercel.json)

```json
{
  "buildCommand": "npm run build",
  "framework": "nextjs",
  "regions": ["iad1"],
  "headers": [
    {
      "source": "/(.*)",
      "headers": [
        {
          "key": "X-Content-Type-Options",
          "value": "nosniff"
        },
        {
          "key": "X-Frame-Options",
          "value": "DENY"
        },
        {
          "key": "X-XSS-Protection",
          "value": "1; mode=block"
        }
      ]
    }
  ]
}
```

---

## MODERN FEATURES CHECKLIST (2026)

- ✅ Next.js 16 with Turbopack
- ✅ React 19.2 with useOptimistic
- ✅ Tailwind CSS v4 (100x faster builds)
- ✅ TypeScript 5.9 strict mode
- ✅ Stripe API 2025-12-15
- ✅ Geist font (Vercel's optimized font)
- ✅ Server Components by default
- ✅ Streaming with Suspense
- ✅ Edge runtime support
- ✅ Image optimization (AVIF/WebP)
- ✅ Accessibility (WCAG 2.2 AA)
- ✅ Core Web Vitals optimization
- ✅ Security headers
- ✅ Structured data (JSON-LD)

---

## NOTES

All services data, testimonials, and business information remain the same as the original PRD.

This PRD uses **2026 cutting-edge technology** while maintaining backward compatibility and production stability.

**Target Performance:**
- Lighthouse: 95+ (all categories)
- First Contentful Paint: < 1.2s
- Time to Interactive: < 2.5s
- Cumulative Layout Shift: < 0.1
