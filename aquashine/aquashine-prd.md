# AquaShine Pool Services - Complete Website PRD

## OVERVIEW

Build a complete, production-ready pool services website for AquaShine Pool Services. The website must support both subscription-based recurring payments and one-time payments through Stripe Checkout. The site should be professional, mobile-first, fast, and conversion-optimized.

**This is a COMPLETE specification. Implement EVERYTHING described below without asking questions.**

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

## TECH STACK (MANDATORY)

```
Framework: Next.js 14 (App Router)
Language: TypeScript (strict mode)
Styling: Tailwind CSS
Payments: Stripe Checkout
Icons: Lucide React
Form Handling: React Hook Form with Zod validation
Font: Inter (from next/font/google)
```

### Package.json Dependencies

```json
{
  "dependencies": {
    "next": "14.x",
    "react": "18.x",
    "react-dom": "18.x",
    "stripe": "^14.0.0",
    "@stripe/stripe-js": "^2.0.0",
    "lucide-react": "^0.300.0",
    "react-hook-form": "^7.49.0",
    "@hookform/resolvers": "^3.3.0",
    "zod": "^3.22.0"
  },
  "devDependencies": {
    "typescript": "^5.0.0",
    "@types/node": "^20.0.0",
    "@types/react": "^18.0.0",
    "@types/react-dom": "^18.0.0",
    "tailwindcss": "^3.4.0",
    "postcss": "^8.0.0",
    "autoprefixer": "^10.0.0",
    "eslint": "^8.0.0",
    "eslint-config-next": "14.x"
  }
}
```

---

## DESIGN SYSTEM

### Color Palette (Tailwind Config)

```javascript
// tailwind.config.ts
const config = {
  theme: {
    extend: {
      colors: {
        primary: {
          50: '#EBF8FF',
          100: '#CAF0F8',
          200: '#90E0EF',
          300: '#00B4D8',
          400: '#0096C7',
          500: '#0077B6',
          600: '#005F8A',
          700: '#004A6E',
          800: '#003652',
          900: '#03045E',
        },
        accent: {
          DEFAULT: '#03045E',
          light: '#023E8A',
        }
      },
      fontFamily: {
        sans: ['var(--font-inter)', 'system-ui', 'sans-serif'],
      },
    },
  },
}
```

### Typography Scale

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

### Component Styles

```
Button Primary: 
  bg-primary-500 hover:bg-primary-600 text-white 
  px-6 py-3 rounded-lg font-semibold 
  transition-all duration-200 
  shadow-md hover:shadow-lg
  focus:outline-none focus:ring-2 focus:ring-primary-500 focus:ring-offset-2

Button Secondary:
  bg-white hover:bg-gray-50 text-primary-500 
  border-2 border-primary-500
  px-6 py-3 rounded-lg font-semibold
  transition-all duration-200

Button Ghost:
  text-primary-500 hover:bg-primary-50
  px-6 py-3 rounded-lg font-semibold
  transition-all duration-200

Card:
  bg-white rounded-2xl shadow-lg 
  border border-gray-100
  hover:shadow-xl transition-shadow duration-300

Input:
  w-full px-4 py-3 rounded-lg
  border border-gray-300 
  focus:border-primary-500 focus:ring-2 focus:ring-primary-500/20
  transition-all duration-200
  placeholder:text-gray-400

Badge:
  inline-flex items-center px-3 py-1 
  rounded-full text-sm font-medium
  
Badge Subscription: bg-primary-100 text-primary-700
Badge One-Time: bg-green-100 text-green-700
Badge Popular: bg-amber-100 text-amber-700
```

### Shadows

```
shadow-sm: 0 1px 2px 0 rgb(0 0 0 / 0.05)
shadow: 0 1px 3px 0 rgb(0 0 0 / 0.1), 0 1px 2px -1px rgb(0 0 0 / 0.1)
shadow-md: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1)
shadow-lg: 0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1)
shadow-xl: 0 20px 25px -5px rgb(0 0 0 / 0.1), 0 8px 10px -6px rgb(0 0 0 / 0.1)
```

---

## FILE STRUCTURE

```
aquashine/
├── .env.local                    # Environment variables (create this)
├── .env.example                  # Example env file
├── next.config.js
├── tailwind.config.ts
├── tsconfig.json
├── package.json
├── public/
│   ├── favicon.ico
│   ├── og-image.jpg             # 1200x630 placeholder
│   └── images/
│       └── pool-hero.jpg        # Hero background placeholder
├── src/
│   ├── app/
│   │   ├── layout.tsx           # Root layout
│   │   ├── page.tsx             # Home page
│   │   ├── globals.css          # Global styles
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
│   │           └── route.ts     # Stripe checkout API
│   ├── components/
│   │   ├── layout/
│   │   │   ├── Header.tsx       # Site header
│   │   │   ├── Footer.tsx       # Site footer
│   │   │   ├── MobileMenu.tsx   # Mobile navigation
│   │   │   └── Container.tsx    # Container wrapper
│   │   ├── home/
│   │   │   ├── Hero.tsx         # Hero section
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
│   └── types/
│       └── index.ts             # TypeScript types
```

---

## TYPES (src/types/index.ts)

```typescript
export interface Service {
  id: string;
  name: string;
  shortName: string;
  price: number;
  unit: 'week' | 'visit' | 'one-time';
  type: 'subscription' | 'one_time';
  interval?: 'week' | 'month';
  description: string;
  shortDescription: string;
  includes: string[];
  popular?: boolean;
  icon: string;
}

export interface Testimonial {
  id: string;
  name: string;
  location: string;
  text: string;
  rating: number;
}

export interface ContactFormData {
  name: string;
  email: string;
  phone: string;
  address?: string;
  service?: string;
  message: string;
}

export interface CheckoutRequest {
  serviceId: string;
  serviceName: string;
  price: number;
  type: 'subscription' | 'one_time';
  interval?: 'week' | 'month';
}

export interface NavLink {
  label: string;
  href: string;
}

export interface Feature {
  icon: string;
  title: string;
  description: string;
}
```

---

## DATA (src/data/services.ts)

```typescript
import { Service, Testimonial, Feature, NavLink } from '@/types';

export const services: Service[] = [
  {
    id: 'weekly-maintenance',
    name: 'Weekly Pool Maintenance',
    shortName: 'Weekly Maintenance',
    price: 35,
    unit: 'week',
    type: 'subscription',
    interval: 'week',
    description: 'Our most comprehensive service. We visit every week to keep your pool in perfect condition year-round. Never worry about your pool again.',
    shortDescription: 'Complete weekly care for a pristine pool all year.',
    includes: [
      'Skim surface and remove all debris',
      'Vacuum pool floor and walls',
      'Brush walls, tiles, and steps',
      'Test water chemistry (pH, chlorine, alkalinity)',
      'Balance and add chemicals as needed',
      'Clean skimmer and pump baskets',
      'Backwash filter as needed',
      'Inspect pump, filter, and equipment',
      'Check water level and adjust',
      'Written service report after each visit'
    ],
    popular: true,
    icon: 'Calendar'
  },
  {
    id: 'biweekly-maintenance',
    name: 'Bi-Weekly Pool Maintenance',
    shortName: 'Bi-Weekly Maintenance',
    price: 45,
    unit: 'visit',
    type: 'subscription',
    interval: 'week',
    description: 'Perfect for covered pools, screened enclosures, or pools with lighter use. All the essentials, twice a month.',
    shortDescription: 'Essential maintenance every two weeks.',
    includes: [
      'Skim surface and remove debris',
      'Vacuum pool floor',
      'Brush walls and tiles',
      'Test and balance water chemistry',
      'Add chemicals as needed',
      'Clean skimmer and pump baskets',
      'Basic equipment inspection',
      'Service report'
    ],
    popular: false,
    icon: 'CalendarDays'
  },
  {
    id: 'deep-clean',
    name: 'One-Time Deep Clean',
    shortName: 'Deep Clean',
    price: 175,
    unit: 'one-time',
    type: 'one_time',
    description: 'Restore your neglected or dirty pool to sparkling condition. Perfect before a party, after a storm, or if your pool needs extra attention.',
    shortDescription: 'Restore your pool to pristine condition.',
    includes: [
      'Complete debris removal (surface and bottom)',
      'Thorough vacuuming of entire pool',
      'Brush all surfaces including tile line',
      'Acid wash tile line (if needed)',
      'Clean and degrease filter',
      'Shock treatment',
      'Full chemical balance',
      'Clean all baskets and skimmers',
      'Equipment inspection and report',
      'Before and after water test'
    ],
    popular: false,
    icon: 'Sparkles'
  },
  {
    id: 'pool-opening',
    name: 'Seasonal Pool Opening',
    shortName: 'Pool Opening',
    price: 250,
    unit: 'one-time',
    type: 'one_time',
    description: 'Get your pool ready for swim season. We handle everything to get your pool from closed to swim-ready.',
    shortDescription: 'Complete pool opening for swim season.',
    includes: [
      'Remove and fold winter cover',
      'Clean and store cover (customer storage)',
      'Reinstall ladders, rails, and accessories',
      'Inspect and reconnect all equipment',
      'Prime and start pump',
      'Check for leaks',
      'Shock treatment',
      'Full chemical balance',
      'Skim and vacuum',
      'Equipment test and inspection report'
    ],
    popular: false,
    icon: 'Sun'
  },
  {
    id: 'pool-closing',
    name: 'Seasonal Pool Closing',
    shortName: 'Pool Closing',
    price: 250,
    unit: 'one-time',
    type: 'one_time',
    description: 'Properly winterize your pool to prevent damage and expensive repairs. Peace of mind for the off-season.',
    shortDescription: 'Professional winterization service.',
    includes: [
      'Lower water level to proper height',
      'Blow out all plumbing lines',
      'Add antifreeze to lines',
      'Add winterizing chemicals',
      'Drain pump, filter, and heater',
      'Remove and store ladders/accessories',
      'Install winter plugs',
      'Install winter cover (if provided)',
      'Final equipment inspection',
      'Winterization checklist provided'
    ],
    popular: false,
    icon: 'Snowflake'
  },
  {
    id: 'chemical-balance',
    name: 'Chemical Balance Service',
    shortName: 'Chemical Balance',
    price: 50,
    unit: 'one-time',
    type: 'one_time',
    description: 'Professional water testing and chemical adjustment. Ensure your pool water is safe, clear, and balanced.',
    shortDescription: 'Expert water testing and balancing.',
    includes: [
      'Comprehensive 7-point water test',
      'pH level adjustment',
      'Chlorine/sanitizer optimization',
      'Total alkalinity balancing',
      'Calcium hardness adjustment',
      'Cyanuric acid (stabilizer) check',
      'Add all necessary chemicals',
      'Written water quality report'
    ],
    popular: false,
    icon: 'TestTube'
  },
  {
    id: 'green-pool-recovery',
    name: 'Green Pool Recovery',
    shortName: 'Green Pool Recovery',
    price: 299,
    unit: 'one-time',
    type: 'one_time',
    description: 'Is your pool green? We\'ll bring it back to crystal clear. Our green pool recovery service handles even the worst algae blooms.',
    shortDescription: 'Transform your green pool to crystal clear.',
    includes: [
      'Initial assessment and water test',
      'Debris removal',
      'Heavy shock treatment',
      'Algaecide application',
      'Filter cleaning (multiple times)',
      'Daily monitoring (3-5 days)',
      'Multiple chemical treatments',
      'Final vacuum and brush',
      'Water clarity guarantee',
      'Maintenance recommendations'
    ],
    popular: false,
    icon: 'Leaf'
  },
  {
    id: 'equipment-inspection',
    name: 'Equipment Inspection',
    shortName: 'Equipment Inspection',
    price: 75,
    unit: 'one-time',
    type: 'one_time',
    description: 'Comprehensive inspection of all pool equipment. Identify problems before they become expensive repairs.',
    shortDescription: 'Complete equipment health check.',
    includes: [
      'Pump inspection and flow test',
      'Filter pressure and condition check',
      'Heater inspection (if applicable)',
      'Salt cell inspection (if applicable)',
      'Timer and automation check',
      'Valve operation test',
      'Leak detection (visual)',
      'Electrical connection check',
      'Detailed written report',
      'Repair recommendations with estimates'
    ],
    popular: false,
    icon: 'Wrench'
  }
];

export const testimonials: Testimonial[] = [
  {
    id: '1',
    name: 'Maria Rodriguez',
    location: 'Orlando, FL',
    text: 'AquaShine has been maintaining our pool for 6 months and it has never looked better. They show up on time every week and are always professional. Highly recommend to anyone in the Orlando area!',
    rating: 5
  },
  {
    id: '2',
    name: 'James Thompson',
    location: 'Kissimmee, FL',
    text: 'Finally found a reliable pool service! After trying three other companies, AquaShine is the only one that consistently shows up and does a thorough job. Worth every penny.',
    rating: 5
  },
  {
    id: '3',
    name: 'Sarah Mitchell',
    location: 'Winter Garden, FL',
    text: 'Great communication and fair pricing. I get a text when they\'re on the way and a report after each visit. Our pool is always crystal clear. The kids love it!',
    rating: 5
  },
  {
    id: '4',
    name: 'David Chen',
    location: 'Lake Nona, FL',
    text: 'Called them for a green pool recovery - it was BAD. Within 4 days they had it looking like new. Now they do our weekly maintenance. Excellent service all around.',
    rating: 5
  },
  {
    id: '5',
    name: 'Jennifer Adams',
    location: 'Winter Park, FL',
    text: 'We switched from a big franchise company to AquaShine and the difference is night and day. Personal service, better results, and they actually care about our pool.',
    rating: 5
  },
  {
    id: '6',
    name: 'Robert Martinez',
    location: 'Windermere, FL',
    text: 'Professional, punctual, and thorough. They caught a small pump issue during a routine visit that could have been a major repair. Saved us hundreds of dollars.',
    rating: 5
  }
];

export const features: Feature[] = [
  {
    icon: 'Shield',
    title: 'Licensed & Insured',
    description: 'Fully licensed and insured for your complete peace of mind. We carry comprehensive liability coverage.'
  },
  {
    icon: 'Clock',
    title: 'Reliable Service',
    description: 'We show up on time, every time. You\'ll receive a notification when we\'re on our way to your home.'
  },
  {
    icon: 'DollarSign',
    title: 'Transparent Pricing',
    description: 'No hidden fees, no surprise charges. The price you see is the price you pay, guaranteed.'
  },
  {
    icon: 'MapPin',
    title: 'Locally Owned',
    description: 'Proudly serving Central Florida. We live here, we work here, and we care about our community.'
  },
  {
    icon: 'Award',
    title: 'Experienced Team',
    description: 'Our technicians are trained professionals with years of pool care experience.'
  },
  {
    icon: 'MessageSquare',
    title: 'Great Communication',
    description: 'Service reports after every visit. Questions? We respond within hours, not days.'
  }
];

export const navLinks: NavLink[] = [
  { label: 'Home', href: '/' },
  { label: 'Services', href: '/services' },
  { label: 'Book Now', href: '/book' },
  { label: 'Contact', href: '/contact' }
];

export const serviceAreas = [
  'Orlando',
  'Kissimmee',
  'Winter Garden',
  'Winter Park',
  'Windermere',
  'Lake Nona',
  'Dr. Phillips',
  'Ocoee',
  'Celebration',
  'St. Cloud',
  'Apopka',
  'Altamonte Springs',
  'Casselberry',
  'Sanford',
  'Clermont',
  'Davenport'
];

export const businessHours = [
  { day: 'Monday', hours: '8:00 AM - 6:00 PM' },
  { day: 'Tuesday', hours: '8:00 AM - 6:00 PM' },
  { day: 'Wednesday', hours: '8:00 AM - 6:00 PM' },
  { day: 'Thursday', hours: '8:00 AM - 6:00 PM' },
  { day: 'Friday', hours: '8:00 AM - 6:00 PM' },
  { day: 'Saturday', hours: '9:00 AM - 4:00 PM' },
  { day: 'Sunday', hours: 'Closed' }
];

export const contactInfo = {
  phone: '917-340-6578',
  phoneFormatted: '(917) 340-6578',
  phoneLink: 'tel:+19173406578',
  email: 'info@aquashinepools.com',
  emailLink: 'mailto:info@aquashinepools.com'
};
```

---

## STRIPE CONFIGURATION

### lib/stripe.ts (Server)

```typescript
import Stripe from 'stripe';

if (!process.env.STRIPE_SECRET_KEY) {
  throw new Error('STRIPE_SECRET_KEY is not set in environment variables');
}

export const stripe = new Stripe(process.env.STRIPE_SECRET_KEY, {
  apiVersion: '2023-10-16',
  typescript: true,
});
```

### lib/stripe-client.ts (Client)

```typescript
import { loadStripe, Stripe } from '@stripe/stripe-js';

let stripePromise: Promise<Stripe | null>;

export const getStripe = () => {
  if (!stripePromise) {
    stripePromise = loadStripe(process.env.NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY!);
  }
  return stripePromise;
};
```

### Environment Variables (.env.local)

```
# Stripe Keys (use test keys for development)
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_test_YOUR_KEY_HERE
STRIPE_SECRET_KEY=sk_test_YOUR_KEY_HERE

# Base URL
NEXT_PUBLIC_BASE_URL=http://localhost:3000
```

### Environment Example (.env.example)

```
# Stripe Keys
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_test_xxxxxxxxxxxxxxxxxxxxxxxxxxxxx
STRIPE_SECRET_KEY=sk_test_xxxxxxxxxxxxxxxxxxxxxxxxxxxxx

# Base URL (change to production URL when deploying)
NEXT_PUBLIC_BASE_URL=http://localhost:3000
```

---

## API ROUTE (src/app/api/checkout/route.ts)

```typescript
import { NextRequest, NextResponse } from 'next/server';
import { stripe } from '@/lib/stripe';
import { services } from '@/data/services';

export async function POST(request: NextRequest) {
  try {
    const body = await request.json();
    const { serviceId } = body;

    // Find the service
    const service = services.find((s) => s.id === serviceId);
    
    if (!service) {
      return NextResponse.json(
        { error: 'Service not found' },
        { status: 404 }
      );
    }

    const baseUrl = process.env.NEXT_PUBLIC_BASE_URL || 'http://localhost:3000';

    // Create checkout session based on service type
    if (service.type === 'subscription') {
      // Create a subscription checkout session
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
              unit_amount: service.price * 100, // Convert to cents
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
      });

      return NextResponse.json({ url: session.url });
    } else {
      // Create a one-time payment checkout session
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
              unit_amount: service.price * 100, // Convert to cents
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
      });

      return NextResponse.json({ url: session.url });
    }
  } catch (error) {
    console.error('Checkout error:', error);
    return NextResponse.json(
      { error: 'Failed to create checkout session' },
      { status: 500 }
    );
  }
}
```

---

## UTILITY FUNCTIONS (src/lib/utils.ts)

```typescript
import { type ClassValue, clsx } from 'clsx';
import { twMerge } from 'tailwind-merge';

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}

export function formatPrice(price: number): string {
  return new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD',
    minimumFractionDigits: 0,
    maximumFractionDigits: 0,
  }).format(price);
}

export function formatPhoneNumber(phone: string): string {
  const cleaned = phone.replace(/\D/g, '');
  const match = cleaned.match(/^(\d{3})(\d{3})(\d{4})$/);
  if (match) {
    return `(${match[1]}) ${match[2]}-${match[3]}`;
  }
  return phone;
}
```

**Note:** Also install clsx and tailwind-merge:
```bash
npm install clsx tailwind-merge
```

---

## PAGE SPECIFICATIONS

### Root Layout (src/app/layout.tsx)

```typescript
import type { Metadata } from 'next';
import { Inter } from 'next/font/google';
import './globals.css';
import Header from '@/components/layout/Header';
import Footer from '@/components/layout/Footer';

const inter = Inter({ 
  subsets: ['latin'],
  variable: '--font-inter',
});

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
};

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en" className={inter.variable}>
      <body className="min-h-screen flex flex-col bg-white text-gray-900 antialiased">
        <Header />
        <main className="flex-grow">{children}</main>
        <Footer />
      </body>
    </html>
  );
}
```

---

### Home Page (src/app/page.tsx)

**Sections in order:**
1. Hero
2. Services Preview (3 featured services)
3. Why Choose Us (6 features in grid)
4. Testimonials (carousel or grid of 3)
5. Service Areas
6. Final CTA

**Hero Section Specifications:**
- Full viewport height on mobile, 80vh on desktop minimum
- Background: Gradient from primary-900 to primary-700 with subtle pattern overlay
- Content centered vertically and horizontally
- H1: "Crystal Clear Pools, Zero Hassle"
- Subheading: "Professional pool maintenance for Orlando, Kissimmee & Central Florida. Sit back, relax, and enjoy your pool while we handle the rest."
- Two CTA buttons side by side:
  - Primary: "View Our Services" → /services
  - Secondary (white outline): "Book Now" → /book
- Below buttons: Phone number with icon "Call Now: (917) 340-6578"
- Subtle scroll indicator at bottom

**Services Preview Section:**
- Light gray background (gray-50)
- Section title: "Our Services"
- Section subtitle: "Everything you need to keep your pool perfect"
- 3 cards in a row (responsive grid)
- Featured services: Weekly Maintenance (with "Most Popular" badge), Deep Clean, Chemical Balance
- Each card: icon, name, price, short description, "Learn More" link
- Bottom: "View All Services" button → /services

**Why Choose Us Section:**
- White background
- Section title: "Why Orlando Chooses AquaShine"
- Section subtitle: "We're not just another pool company"
- 6 feature cards in 2x3 grid (3x2 on mobile)
- Each card: Large icon (primary color), title, description
- Clean, minimal design

**Testimonials Section:**
- Light blue background (primary-50)
- Section title: "What Our Customers Say"
- Section subtitle: "Don't just take our word for it"
- 3 testimonial cards
- Each card: Quote text, 5-star rating, customer name, location
- Cards have white background with shadow

**Service Areas Section:**
- White background
- Section title: "Areas We Serve"
- Section subtitle: "Proudly serving Central Florida"
- Display service areas in a flowing grid/tag layout
- Map placeholder or icon
- "Don't see your area? Call us!" with phone number

**Final CTA Section:**
- Primary blue gradient background
- H2: "Ready for a Cleaner Pool?"
- Text: "Get started today with Orlando's trusted pool service"
- Two buttons: "Book Your Service" and "Call (917) 340-6578"

---

### Services Page (src/app/services/page.tsx)

**Metadata:**
```typescript
export const metadata: Metadata = {
  title: 'Pool Cleaning Services',
  description: 'Complete pool cleaning and maintenance services in Orlando and Kissimmee. Weekly maintenance, deep cleaning, pool opening/closing, and more.',
};
```

**Page Structure:**
- Hero section (smaller than home)
  - H1: "Our Pool Services"
  - Subtitle: "Comprehensive pool care solutions for every need and budget"
  - Background: Gradient or solid primary color

- Services Grid
  - All 8 services displayed
  - 2 columns on desktop, 1 on mobile
  - Each service is a full card with:
    - Icon
    - Service name
    - Price with unit (e.g., "$35/week" or "$175 one-time")
    - Badge for type (Subscription or One-Time)
    - "Most Popular" badge for weekly maintenance
    - Full description
    - "What's Included" expandable or visible list
    - "Book This Service" button → /book?service={id}

- Bottom CTA
  - "Not sure which service you need?"
  - "Call us at (917) 340-6578 for a free consultation"
  - Or link to contact page

---

### Book Now Page (src/app/book/page.tsx)

**Metadata:**
```typescript
export const metadata: Metadata = {
  title: 'Book Your Pool Service',
  description: 'Book professional pool cleaning services online. Easy scheduling, secure payment, and service confirmation.',
};
```

**Page Structure:**
- Hero section (small)
  - H1: "Book Your Service"
  - Subtitle: "Select a service below to get started. Secure checkout powered by Stripe."

- Service Selection Grid
  - All services as booking cards
  - 2 columns on desktop, 1 on mobile
  - Each card shows:
    - Service name
    - Price (formatted appropriately for type)
    - Short description
    - Type badge (Subscription/One-Time)
    - "Book Now" button
  - Popular service highlighted with border or badge

- URL Parameter Handling
  - If `?service={serviceId}` is in URL, that service card should be highlighted/scrolled to
  - Auto-scroll to that service on page load

- Booking Flow (onClick):
  1. Show loading state on button
  2. POST to /api/checkout with serviceId
  3. Receive Stripe Checkout URL
  4. Redirect to Stripe Checkout
  5. On success → /success
  6. On cancel → /canceled

- Trust Signals below grid:
  - "Secure checkout powered by Stripe"
  - "Cancel anytime for subscriptions"
  - "Satisfaction guaranteed"

- Alternative Contact:
  - "Prefer to talk first?"
  - Phone number and contact page link

---

### Contact Page (src/app/contact/page.tsx)

**Metadata:**
```typescript
export const metadata: Metadata = {
  title: 'Contact Us',
  description: 'Contact AquaShine Pool Services. Call (917) 340-6578 or fill out our contact form. Serving Orlando, Kissimmee, and Central Florida.',
};
```

**Page Structure:**
- Hero section (small)
  - H1: "Contact Us"
  - Subtitle: "We'd love to hear from you. Reach out anytime."

- Two Column Layout (stack on mobile):

**Left Column - Contact Form:**
- Fields:
  - Name (text, required)
  - Email (email, required)
  - Phone (tel, required)
  - Service Address (text, optional, placeholder: "Where is your pool located?")
  - Service Interested In (select dropdown, optional)
    - Options: All service names + "Not sure / General inquiry"
  - Message (textarea, required, min 10 characters)
- Submit button: "Send Message"
- Form validation with Zod
- On submit:
  - Show loading state
  - Simulate submission (setTimeout 1.5s)
  - Show success message: "Thanks! We'll get back to you within 24 hours."
  - Reset form
- Note: Actual form backend not required for MVP. Just show success UI.

**Right Column - Contact Information:**
- Phone Section:
  - Icon + "Call Us"
  - Phone number (large, clickable link)
  - "Mon-Fri: 8am-6pm, Sat: 9am-4pm"

- Email Section:
  - Icon + "Email Us"
  - Email address (clickable mailto link)
  - "We respond within 24 hours"

- Service Areas Section:
  - Icon + "Areas We Serve"
  - List all service areas in 2-3 columns
  - "Don't see your area? Contact us!"

- Business Hours Section:
  - Icon + "Business Hours"
  - Full hours list
  - Note: "Emergency service available"

---

### Success Page (src/app/success/page.tsx)

**Metadata:**
```typescript
export const metadata: Metadata = {
  title: 'Booking Confirmed',
  description: 'Your pool service booking has been confirmed.',
};
```

**Page Structure:**
- Centered content
- Large success icon (green checkmark in circle)
- H1: "Thank You!"
- H2: "Your Booking is Confirmed"
- Text: "We've received your booking and will be in touch within 24 hours to confirm your service details and schedule."
- If subscription: "Your subscription is now active. You'll be billed automatically according to your service schedule."
- If one-time: "We'll contact you shortly to schedule your service at a time that works for you."
- Box with next steps:
  1. "Check your email for a confirmation receipt"
  2. "We'll call or text to confirm your service date"
  3. "Make sure your pool area is accessible"
- Contact info: "Questions? Call us at (917) 340-6578"
- Button: "Return to Home" → /

---

### Canceled Page (src/app/canceled/page.tsx)

**Metadata:**
```typescript
export const metadata: Metadata = {
  title: 'Booking Canceled',
  description: 'Your pool service booking was canceled.',
};
```

**Page Structure:**
- Centered content
- Icon (info circle, blue)
- H1: "Booking Canceled"
- Text: "No worries! Your booking was not processed and you have not been charged."
- Text: "If you experienced any issues or have questions, we're here to help."
- Contact info: "Call us at (917) 340-6578 or email info@aquashinepools.com"
- Two buttons:
  - Primary: "Try Again" → /book
  - Secondary: "Return to Home" → /

---

## COMPONENT SPECIFICATIONS

### Header Component

**Desktop (lg and up):**
- Fixed/sticky at top
- White background with subtle shadow on scroll
- Left: Logo/Business name "AquaShine" (link to home)
  - Icon: Droplets or Water icon from Lucide
  - Text in primary-600, bold
- Center/Right: Navigation links (Home, Services, Book Now, Contact)
  - Normal state: text-gray-600
  - Hover: text-primary-500
  - Active: text-primary-600, font-medium
- Far Right: Phone number with phone icon
  - Clickable tel: link
  - "917-340-6578"
- Far Right: "Book Now" button (primary style, smaller)

**Mobile (below lg):**
- Fixed/sticky at top
- White background
- Left: Logo "AquaShine"
- Right: Hamburger menu icon
- Mobile menu (slides in from right or drops down):
  - All nav links stacked
  - Phone number
  - "Book Now" button
  - Close button

**Scroll Behavior:**
- Add shadow when scrolled past 50px
- Can optionally shrink padding slightly on scroll

### Footer Component

**Structure:**
- Dark background (primary-900 or accent)
- Padding: py-12 md:py-16

**Desktop Layout (4 columns):**
1. Column 1 - Brand:
   - AquaShine logo
   - Tagline: "Crystal Clear Pools, Zero Hassle"
   - Brief text: "Professional pool maintenance serving Orlando, Kissimmee, and Central Florida."

2. Column 2 - Quick Links:
   - Heading: "Quick Links"
   - Home, Services, Book Now, Contact

3. Column 3 - Services:
   - Heading: "Services"
   - Weekly Maintenance, Deep Clean, Pool Opening, Pool Closing, Chemical Balance

4. Column 4 - Contact:
   - Heading: "Contact Us"
   - Phone: (917) 340-6578
   - Email: info@aquashinepools.com
   - Areas: Orlando, Kissimmee & Central FL

**Bottom Bar:**
- Separator line
- Left: "© 2025 AquaShine Pool Services. All rights reserved."
- Right: Optional links (Privacy Policy, Terms of Service) - can be placeholders

**Mobile Layout:**
- Stack all columns vertically
- Reduce to 2 columns or single column
- Center-align text on mobile

---

## GLOBAL STYLES (src/app/globals.css)

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  html {
    scroll-behavior: smooth;
  }
  
  body {
    @apply text-gray-900 bg-white;
  }
  
  h1, h2, h3, h4, h5, h6 {
    @apply font-bold tracking-tight text-gray-900;
  }
}

@layer components {
  .section-padding {
    @apply py-16 md:py-20 lg:py-24;
  }
  
  .container-custom {
    @apply max-w-7xl mx-auto px-4 sm:px-6 lg:px-8;
  }
  
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
  
  .btn-white {
    @apply inline-flex items-center justify-center
           bg-white hover:bg-gray-100
           text-primary-600 font-semibold
           px-6 py-3 rounded-lg
           transition-all duration-200
           shadow-md hover:shadow-lg;
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
  
  .section-title {
    @apply text-3xl md:text-4xl font-bold text-center text-gray-900;
  }
  
  .section-subtitle {
    @apply text-lg text-gray-600 text-center mt-4 max-w-2xl mx-auto;
  }
}

@layer utilities {
  .text-balance {
    text-wrap: balance;
  }
}
```

---

## SEO REQUIREMENTS

**Every page must have:**
1. Unique title tag (via metadata)
2. Meta description (via metadata)
3. Proper heading hierarchy (one H1, then H2s, H3s)
4. Semantic HTML (header, main, footer, nav, section, article)
5. Alt text on all images (use descriptive text)
6. Canonical URL (handled by Next.js)

**Structured Data (optional but recommended):**
Add LocalBusiness schema to the home page:

```typescript
// Add to layout.tsx or page.tsx
const structuredData = {
  "@context": "https://schema.org",
  "@type": "LocalBusiness",
  "name": "AquaShine Pool Services",
  "description": "Professional pool cleaning and maintenance services in Orlando, Kissimmee, and Central Florida.",
  "telephone": "+1-917-340-6578",
  "email": "info@aquashinepools.com",
  "areaServed": ["Orlando", "Kissimmee", "Winter Garden", "Winter Park", "Lake Nona"],
  "priceRange": "$$",
  "address": {
    "@type": "PostalAddress",
    "addressLocality": "Orlando",
    "addressRegion": "FL",
    "addressCountry": "US"
  }
};
```

---

## RESPONSIVE BREAKPOINTS

Follow Tailwind defaults:
- sm: 640px
- md: 768px
- lg: 1024px
- xl: 1280px
- 2xl: 1536px

**Key responsive behaviors:**
- Navigation: Hamburger menu below lg (1024px)
- Grids: 1 column mobile, 2 columns tablet, 2-4 columns desktop
- Hero: Stack elements on mobile, side-by-side on desktop
- Footer: 1-2 columns mobile, 4 columns desktop
- Text sizes: Scale up on larger screens
- Padding: Increase on larger screens

---

## ACCESSIBILITY REQUIREMENTS

1. All interactive elements must be keyboard accessible
2. Proper focus states on all buttons and links
3. Sufficient color contrast (WCAG AA minimum)
4. Form labels associated with inputs
5. Error messages announced to screen readers
6. Skip to main content link (optional)
7. ARIA labels where needed
8. Reduced motion support (respect prefers-reduced-motion)

---

## PERFORMANCE REQUIREMENTS

1. Use Next.js Image component for all images
2. Lazy load below-fold content
3. Minimize client-side JavaScript
4. Use Server Components where possible
5. Optimize fonts with next/font
6. Target Lighthouse score: 90+ on all metrics

---

## TESTING CHECKLIST

Before considering complete, verify:

- [ ] All pages render without errors
- [ ] Navigation works on all pages
- [ ] Mobile menu opens and closes
- [ ] All links work correctly
- [ ] Contact form shows validation errors
- [ ] Contact form shows success message
- [ ] Book Now buttons trigger Stripe checkout
- [ ] Stripe checkout loads correctly (test mode)
- [ ] Success page displays after payment
- [ ] Canceled page displays if user backs out
- [ ] Site is fully responsive (test at 320px, 768px, 1024px, 1440px)
- [ ] No horizontal scroll on any page
- [ ] All text is readable
- [ ] Phone numbers are clickable on mobile
- [ ] Footer links work
- [ ] Images load (or placeholders display)

---

## DEPLOYMENT NOTES

**For Vercel deployment:**
1. Push to GitHub
2. Connect repo to Vercel
3. Add environment variables in Vercel dashboard:
   - NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY
   - STRIPE_SECRET_KEY
   - NEXT_PUBLIC_BASE_URL (set to production URL)
4. Deploy

**Stripe Production:**
1. Complete Stripe account verification
2. Replace test keys with live keys
3. Set up webhook endpoints (for subscription management)
4. Enable card payments in Stripe dashboard

---

## FUTURE ENHANCEMENTS (NOT IN SCOPE FOR MVP)

- Customer portal for subscription management
- Email notifications (via Resend or SendGrid)
- Actual contact form backend (save to database or email)
- Blog for SEO
- Online scheduling with calendar integration
- Customer reviews integration (Google Reviews)
- Live chat widget
- Service area map with Google Maps

---

## IMPLEMENTATION ORDER

Build in this order:
1. Project setup and configuration (Tailwind, TypeScript, etc.)
2. Types and data files
3. Utility functions and Stripe config
4. Global styles
5. Layout components (Header, Footer)
6. UI components (Button, Card, Badge, Input)
7. Home page with all sections
8. Services page
9. Book page with Stripe integration
10. Contact page
11. Success and Canceled pages
12. API route for checkout
13. Final testing and polish

---

## FINAL NOTES

- Use placeholder images where needed (solid color divs or Unsplash placeholders)
- All prices are in USD
- Phone number format: (917) 340-6578 for display, +19173406578 for tel: links
- Business is assumed to be operational 
- No authentication required for MVP
- No database required for MVP
- Contact form just shows success message, no actual email sending

This PRD is COMPLETE. Implement everything as specified without asking questions. If something is ambiguous, make a reasonable decision and proceed.
```

---

