# AquaShine Pool Services - Build TODO (2026 Edition)

**Complete build plan for the AquaShine website using 2026 modern tech stack**

**Stack**: Next.js 16.1 • React 19.2 • TypeScript 5.9 • Tailwind v4 • Stripe API 2025-12-15

---

## Git Workflow Strategy

### Branch Structure
```
main (production)
  └── develop (active development)
        ├── feature/core-infrastructure
        ├── feature/design-system
        ├── feature/layout
        ├── feature/home-page
        ├── feature/services-page
        ├── feature/booking-system
        ├── feature/contact-page
        └── feature/confirmation-pages
```

### Commit Points
- **Commit 1**: Initial project setup (after task 6)
- **Commit 2**: Core infrastructure (after task 13)
- **Commit 3**: Design system (after task 21)
- **Commit 4**: Layout components (after task 27)
- **Commit 5**: Home page complete (after task 38)
- **Commit 6**: Services page (after task 46)
- **Commit 7**: Booking system (after task 58)
- **Commit 8**: Contact page (after task 66)
- **Commit 9**: Confirmation pages (after task 72)
- **Commit 10**: Testing fixes (after task 83)
- **Commit 11**: Production release (after task 90)

### Working with Worktrees (Optional)
```bash
# Create multiple worktrees for parallel development
git worktree add ../aquashine-design feature/design-system
git worktree add ../aquashine-layout feature/layout
git worktree add ../aquashine-home feature/home-page

# List all worktrees
git worktree list

# Remove worktree when done
git worktree remove ../aquashine-design
```

---

## Phase 1: Foundation (Tasks 1-6)
**Branch**: `main` → `develop`

- [ ] **Task 1**: Initialize Next.js 16 project with TypeScript and configure base dependencies
  ```bash
  # Create Next.js 16 project with Turbopack
  npx create-next-app@latest aquashine --typescript --tailwind --app --src-dir --turbo
  cd aquashine

  # Install production dependencies
  npm install stripe@^17.5.0 @stripe/stripe-js@^4.13.0
  npm install lucide-react@^0.460.0
  npm install react-hook-form@^7.54.0 @hookform/resolvers@^3.9.1
  npm install zod@^3.23.8
  npm install clsx@^2.1.1 tailwind-merge@^2.6.0
  npm install geist@^1.3.1

  # Install dev dependencies
  npm install -D @types/node@^22.10.2 @types/react@^19.0.1 @types/react-dom@^19.0.2
  npm install -D typescript@^5.9.3
  npm install -D tailwindcss@^4.0.0 @tailwindcss/vite@^4.0.0
  ```

- [ ] **Task 2**: Configure Tailwind CSS v4 with custom color palette and design tokens
  - Use new Tailwind v4 setup in `globals.css` with `@import "tailwindcss"`
  - Define custom colors in `@theme` block
  - Add primary color palette (50-900 shades)
  - Configure Geist Sans font family
  - Remove old `tailwind.config.ts` if generated (v4 uses CSS-based config)

- [ ] **Task 3**: Set up git repository with main and develop branches
  ```bash
  git init
  git add .
  git commit -m "Initial Next.js setup"
  git branch develop
  git checkout develop
  ```

- [ ] **Task 4**: Create environment configuration files (.env.local, .env.example)
  - Create `.env.example` with placeholder keys
  - Create `.env.local` with test Stripe keys
  - Add `.env.local` to `.gitignore`

- [ ] **Task 5**: Configure TypeScript strict mode and Next.js 16 config
  - Enable strict mode in `tsconfig.json`
  - Create `next.config.ts` (TypeScript config)
  - Enable Turbopack optimizations
  - Configure experimental features (dynamicIO)
  - Set up AVIF/WebP image formats
  - Add security headers

- [ ] **Task 6**: **COMMIT**: Initial project setup with config files
  ```bash
  git add .
  git commit -m "chore: initial Next.js 16 setup with Turbopack, React 19, and Tailwind v4"
  ```

---

## Phase 2: Core Infrastructure (Tasks 7-13)
**Branch**: `feature/core-infrastructure`

- [ ] **Task 7**: Create feature branch: feature/core-infrastructure
  ```bash
  git checkout develop
  git checkout -b feature/core-infrastructure
  ```

- [ ] **Task 8**: Build TypeScript types (src/types/index.ts)
  - Create `Service` interface
  - Create `Testimonial` interface
  - Create `ContactFormData` interface
  - Create `CheckoutRequest` interface
  - Create `NavLink` interface
  - Create `Feature` interface

- [ ] **Task 9**: Create services data file (src/data/services.ts)
  - Add all 8 services with complete data
  - Add 6 testimonials
  - Add 6 features for "Why Choose Us"
  - Add navigation links
  - Add service areas array
  - Add business hours array
  - Add contact info object

- [ ] **Task 10**: Build utility functions (src/lib/utils.ts)
  - `cn()` function for className merging
  - `formatPrice()` function
  - `formatPhoneNumber()` function

- [ ] **Task 11**: Set up Stripe server configuration (src/lib/stripe.ts)
  - Import Stripe SDK v17+
  - Configure with secret key from env
  - Set API version to '2025-12-15' (latest)
  - Add app info metadata

- [ ] **Task 12**: Set up Stripe client configuration (src/lib/stripe-client.ts)
  - Import `@stripe/stripe-js`
  - Create `getStripe()` function with promise caching

- [ ] **Task 13**: **COMMIT**: Add core types, data, and utility infrastructure
  ```bash
  git add .
  git commit -m "feat: add core types, data files, and Stripe configuration"
  ```

---

## Phase 3: Design System (Tasks 14-21)
**Branch**: `feature/design-system`

- [ ] **Task 14**: Create feature branch: feature/design-system
  ```bash
  git checkout develop
  git checkout -b feature/design-system
  ```

- [ ] **Task 15**: Build globals.css with Tailwind v4 setup and custom classes
  - Use `@import "tailwindcss"` (new v4 syntax)
  - Define `@theme` block with custom CSS variables
  - Add `@layer base` styles (smooth scroll, body defaults)
  - Add `@layer components` classes (btn-primary, btn-secondary, card, input-field)
  - Add `@layer utilities` for custom utilities
  - Configure Geist Sans font import

- [ ] **Task 16**: Create Button UI component (src/components/ui/Button.tsx)
  - Accept variant prop: 'primary' | 'secondary' | 'white' | 'ghost'
  - Accept size prop: 'sm' | 'md' | 'lg'
  - Support disabled state
  - Support loading state
  - TypeScript with proper props

- [ ] **Task 17**: Create Card UI component (src/components/ui/Card.tsx)
  - Base card styling
  - Optional padding variants
  - Hover effects
  - Children prop

- [ ] **Task 18**: Create Badge UI component (src/components/ui/Badge.tsx)
  - Accept variant prop: 'subscription' | 'one-time' | 'popular'
  - Custom colors per variant
  - Text prop

- [ ] **Task 19**: Create Input UI component (src/components/ui/Input.tsx)
  - Support all input types
  - Error state styling
  - Label support
  - forwardRef for React Hook Form

- [ ] **Task 20**: Create Container wrapper component (src/components/layout/Container.tsx)
  - Max width constraint
  - Responsive padding
  - Optional className prop

- [ ] **Task 21**: **COMMIT**: Add design system components and global styles
  ```bash
  git add .
  git commit -m "feat: implement design system with UI components and global styles"
  ```

---

## Phase 4: Layout System (Tasks 22-28)
**Branch**: `feature/layout`

- [ ] **Task 22**: Create feature branch: feature/layout
  ```bash
  git checkout develop
  git checkout -b feature/layout
  ```

- [ ] **Task 23**: Build Header component with desktop navigation (src/components/layout/Header.tsx)
  - Logo with Droplets icon
  - Desktop navigation links
  - Phone number display
  - Book Now button
  - Sticky/fixed positioning
  - Shadow on scroll effect

- [ ] **Task 24**: Build MobileMenu component (src/components/layout/MobileMenu.tsx)
  - Hamburger menu icon
  - Slide-in/dropdown menu
  - Navigation links stacked
  - Phone number
  - Book Now button
  - Close button
  - Overlay backdrop

- [ ] **Task 25**: Build Footer component with all sections (src/components/layout/Footer.tsx)
  - 4-column layout (responsive)
  - Brand column with logo and tagline
  - Quick Links column
  - Services column
  - Contact column
  - Bottom bar with copyright
  - Dark background (primary-900)

- [ ] **Task 26**: Create root layout with metadata and structure (src/app/layout.tsx)
  - Import Geist Sans font from 'geist/font/sans'
  - Set up comprehensive metadata (title, description, OG tags, Twitter cards)
  - Include Header and Footer components
  - Add main content wrapper with flex layout
  - Apply Geist Sans font variable to html element
  - Add JSON-LD structured data script

- [ ] **Task 27**: Add structured data schema for LocalBusiness
  - Create JSON-LD structured data
  - Include in layout or home page
  - Business name, phone, email, service areas

- [ ] **Task 28**: **COMMIT**: Complete layout components with navigation
  ```bash
  git add .
  git commit -m "feat: add header, footer, and root layout with SEO"
  git checkout develop
  git merge feature/design-system
  git merge feature/layout
  ```

---

## Phase 5: Home Page (Tasks 29-38)
**Branch**: `feature/home-page`

- [ ] **Task 29**: Create feature branch: feature/home-page
  ```bash
  git checkout develop
  git checkout -b feature/home-page
  ```

- [ ] **Task 30**: Build Hero section component (src/components/home/Hero.tsx)
  - Full viewport height on mobile, 80vh on desktop
  - Gradient background (primary-900 to primary-700)
  - H1: "Crystal Clear Pools, Zero Hassle"
  - Subheading text
  - Two CTA buttons (View Services, Book Now)
  - Phone number with icon
  - Scroll indicator

- [ ] **Task 31**: Build ServicesPreview component (src/components/home/ServicesPreview.tsx)
  - Gray background (gray-50)
  - Section title and subtitle
  - 3 featured services in grid (Weekly Maintenance, Deep Clean, Chemical Balance)
  - Service cards with icon, name, price, description
  - "View All Services" button at bottom

- [ ] **Task 32**: Build WhyChooseUs component (src/components/home/WhyChooseUs.tsx)
  - White background
  - Section title: "Why Orlando Chooses AquaShine"
  - 6 feature cards in 2x3 grid
  - Each card: large icon, title, description
  - Use features data from data file

- [ ] **Task 33**: Build Testimonials component (src/components/home/Testimonials.tsx)
  - Light blue background (primary-50)
  - Section title: "What Our Customers Say"
  - 3 testimonial cards
  - Each card: quote, 5-star rating, name, location
  - White cards with shadow

- [ ] **Task 34**: Build HomeCTA component (src/components/home/HomeCTA.tsx)
  - Primary blue gradient background
  - H2: "Ready for a Cleaner Pool?"
  - Supporting text
  - Two buttons: "Book Your Service" and "Call (917) 340-6578"

- [ ] **Task 35**: Assemble home page with all sections (src/app/page.tsx)
  - Import all home components
  - Arrange in correct order
  - Add sections wrapper/spacing

- [ ] **Task 36**: Add service areas section to home page
  - Section title: "Areas We Serve"
  - Display service areas in flowing grid/tag layout
  - "Don't see your area? Call us!" message

- [ ] **Task 37**: Test responsive behavior on all home page sections
  - Test at 320px, 768px, 1024px, 1440px
  - Verify no horizontal scroll
  - Check text readability
  - Test button interactions

- [ ] **Task 38**: **COMMIT**: Complete home page with all sections
  ```bash
  git add .
  git commit -m "feat: complete home page with hero, services, testimonials, and CTA sections"
  ```

---

## Phase 6: Services Page (Tasks 39-46)
**Branch**: `feature/services-page`

- [ ] **Task 39**: Create feature branch: feature/services-page
  ```bash
  git checkout develop
  git checkout -b feature/services-page
  ```

- [ ] **Task 40**: Build ServiceCard component (src/components/services/ServiceCard.tsx)
  - Display icon, name, price with unit
  - Badge for type (Subscription/One-Time)
  - "Most Popular" badge conditional
  - Full description
  - "What's Included" list
  - "Book This Service" button
  - Link to /book?service={id}

- [ ] **Task 41**: Build ServicesList component (src/components/services/ServicesList.tsx)
  - 2-column grid on desktop, 1 on mobile
  - Map through all 8 services
  - Render ServiceCard for each
  - Responsive gap spacing

- [ ] **Task 42**: Create services page with hero and grid (src/app/services/page.tsx)
  - Add page metadata
  - Hero section: "Our Pool Services"
  - Subtitle text
  - Include ServicesList component
  - Bottom CTA section

- [ ] **Task 43**: Add service filtering/categorization (subscription vs one-time)
  - Optional filter buttons or tabs
  - OR visual grouping with headers
  - Highlight subscription vs one-time

- [ ] **Task 44**: Implement expandable 'What's Included' lists
  - Use disclosure/accordion pattern
  - Or display all items expanded
  - Smooth animations

- [ ] **Task 45**: Test service card interactions and responsiveness
  - Click Book button
  - Verify correct service ID in URL
  - Test mobile card layout

- [ ] **Task 46**: **COMMIT**: Complete services page with all service cards
  ```bash
  git add .
  git commit -m "feat: add services page with detailed service cards and booking links"
  git checkout develop
  git merge feature/home-page
  git merge feature/services-page
  ```

---

## Phase 7: Booking System (Tasks 47-58)
**Branch**: `feature/booking-system`

- [ ] **Task 47**: Create feature branch: feature/booking-system
  ```bash
  git checkout develop
  git checkout -b feature/booking-system
  ```

- [ ] **Task 48**: Build BookingCard component (src/components/booking/BookingCard.tsx)
  - Service name and price
  - Short description
  - Type badge
  - "Book Now" button with loading state
  - onClick handler for checkout
  - Popular service highlighted

- [ ] **Task 49**: Build BookingGrid component (src/components/booking/BookingGrid.tsx)
  - 2-column grid on desktop
  - Map through all services
  - Render BookingCard for each
  - Handle service selection

- [ ] **Task 50**: Create Stripe checkout API route (src/app/api/checkout/route.ts)
  - Accept POST requests
  - Extract serviceId from body
  - Find service in data
  - Return 404 if not found
  - Create checkout session based on type

- [ ] **Task 51**: Implement subscription checkout logic in API route
  - Mode: 'subscription'
  - Create price_data with recurring interval
  - Handle weekly (interval: 'week', interval_count: 1)
  - Handle bi-weekly (interval: 'week', interval_count: 2)
  - Collect billing address and phone
  - Add custom field for service address
  - Set success/cancel URLs

- [ ] **Task 52**: Implement one-time payment checkout logic in API route
  - Mode: 'payment'
  - Create price_data without recurring
  - Collect billing address and phone
  - Add custom fields: service address, preferred date
  - Set success/cancel URLs
  - Return session URL

- [ ] **Task 53**: Build book page with service selection (src/app/book/page.tsx)
  - Add page metadata
  - Hero section: "Book Your Service"
  - Include BookingGrid component
  - Add trust signals section
  - Add alternative contact section

- [ ] **Task 54**: Add URL parameter handling for pre-selected services
  - Parse ?service={serviceId} from URL
  - Scroll to/highlight that service
  - Auto-expand if using accordions

- [ ] **Task 55**: Implement Stripe checkout redirect flow with loading states
  - onClick: set loading state on button
  - POST to /api/checkout with serviceId
  - Handle response
  - Redirect to session.url
  - Handle errors with toast/alert

- [ ] **Task 56**: Add trust signals and alternative contact section
  - "Secure checkout powered by Stripe"
  - "Cancel anytime for subscriptions"
  - "Satisfaction guaranteed"
  - Phone number and contact link

- [ ] **Task 57**: Test Stripe checkout flow in test mode
  - Use test card: 4242 4242 4242 4242
  - Test subscription checkout
  - Test one-time checkout
  - Verify redirect to success page
  - Test cancel flow

- [ ] **Task 58**: **COMMIT**: Complete booking system with Stripe integration
  ```bash
  git add .
  git commit -m "feat: implement booking system with Stripe checkout for subscriptions and one-time payments"
  ```

---

## Phase 8: Contact Page (Tasks 59-66)
**Branch**: `feature/contact-page`

- [ ] **Task 59**: Create feature branch: feature/contact-page
  ```bash
  git checkout develop
  git checkout -b feature/contact-page
  ```

- [ ] **Task 60**: Build ContactForm component with validation (src/components/contact/ContactForm.tsx)
  - Use React Hook Form
  - Fields: name, email, phone, address, service dropdown, message
  - Zod schema validation
  - Error message display
  - Submit handler
  - Loading state
  - Success message after submit

- [ ] **Task 61**: Build ContactInfo component (src/components/contact/ContactInfo.tsx)
  - Phone section with icon and clickable link
  - Email section with mailto link
  - Service areas list
  - Business hours display

- [ ] **Task 62**: Create contact page layout (src/app/contact/page.tsx)
  - Add page metadata
  - Hero section: "Contact Us"
  - Two-column layout (stack on mobile)
  - Left: ContactForm
  - Right: ContactInfo

- [ ] **Task 63**: Implement form validation with React Hook Form and Zod
  - Required field validation
  - Email format validation
  - Phone number format validation
  - Message minimum length (10 chars)
  - Real-time error display

- [ ] **Task 64**: Add form submission with success message simulation
  - onSubmit: show loading
  - setTimeout 1.5s to simulate API call
  - Show success message
  - Reset form
  - Note: No actual backend needed for MVP

- [ ] **Task 65**: Add service areas and business hours display
  - Display all service areas in 2-3 columns
  - Format business hours table
  - Add icons

- [ ] **Task 66**: Test contact form validation and error states
  - Test required fields
  - Test email validation
  - Test phone validation
  - Test success flow
  - Test responsive layout

- [ ] **Task 67**: **COMMIT**: Complete contact page with form validation
  ```bash
  git add .
  git commit -m "feat: add contact page with validated form and business information"
  ```

---

## Phase 9: Confirmation Pages (Tasks 68-72)
**Branch**: `feature/confirmation-pages`

- [ ] **Task 68**: Create feature branch: feature/confirmation-pages
  ```bash
  git checkout develop
  git checkout -b feature/confirmation-pages
  ```

- [ ] **Task 69**: Build success page (src/app/success/page.tsx)
  - Add page metadata
  - Large green checkmark icon
  - H1: "Thank You!"
  - H2: "Your Booking is Confirmed"
  - Confirmation message
  - Next steps list (numbered)
  - Contact info
  - "Return to Home" button

- [ ] **Task 70**: Build canceled page (src/app/canceled/page.tsx)
  - Add page metadata
  - Info icon (blue)
  - H1: "Booking Canceled"
  - Message: not charged
  - Contact info if issues
  - Two buttons: "Try Again" and "Return to Home"

- [ ] **Task 71**: Add dynamic content based on service type to success page
  - If subscription: show subscription message
  - If one-time: show scheduling message
  - Parse service from URL params if needed

- [ ] **Task 72**: Test navigation flow from booking through confirmation
  - Complete booking flow
  - Verify success page displays
  - Click cancel in Stripe, verify canceled page
  - Test return navigation buttons

- [ ] **Task 73**: **COMMIT**: Add success and canceled confirmation pages
  ```bash
  git add .
  git commit -m "feat: add payment success and canceled confirmation pages"
  git checkout develop
  git merge feature/booking-system
  git merge feature/contact-page
  git merge feature/confirmation-pages
  ```

---

## Phase 10: Testing & QA (Tasks 74-83)

- [ ] **Task 74**: Run comprehensive cross-browser testing (Chrome, Firefox, Safari)
  - Test all pages in Chrome
  - Test all pages in Firefox
  - Test all pages in Safari (if available)
  - Note any browser-specific issues

- [ ] **Task 75**: Test responsive design at all breakpoints (320px, 768px, 1024px, 1440px)
  - Use browser dev tools
  - Test each page at each breakpoint
  - Verify no horizontal scroll
  - Check text readability and spacing

- [ ] **Task 76**: Verify mobile navigation menu functionality
  - Open mobile menu
  - Click links
  - Close mobile menu
  - Test on actual mobile device if possible

- [ ] **Task 77**: Test all phone number click-to-call links on mobile
  - Click phone links in header
  - Click phone links in footer
  - Click phone links in contact page
  - Verify tel: links work correctly

- [ ] **Task 78**: Verify all internal navigation links work correctly
  - Test header navigation
  - Test footer navigation
  - Test CTA buttons
  - Test service cards links
  - Verify no broken links

- [ ] **Task 79**: Test keyboard navigation and focus states
  - Tab through all interactive elements
  - Verify focus indicators visible
  - Test form navigation
  - Test menu navigation

- [ ] **Task 80**: Run Lighthouse audit for performance, accessibility, SEO
  - Run audit on home page
  - Run audit on services page
  - Run audit on booking page
  - Target 95+ on all metrics (2026 standards)
  - Verify Core Web Vitals (LCP < 2.5s, FID < 100ms, CLS < 0.1)
  - Check WCAG 2.2 Level AA compliance
  - Note and fix any issues

- [ ] **Task 81**: Optimize images and add placeholder images
  - Add pool-hero.jpg placeholder
  - Add og-image.jpg (1200x630)
  - Use Next.js Image component
  - Add proper alt text

- [ ] **Task 82**: Verify all metadata and SEO tags are correct
  - Check title tags on all pages
  - Check meta descriptions
  - Verify OG tags
  - Check structured data

- [ ] **Task 83**: Test complete Stripe checkout flow with test cards
  - Test successful payment: 4242 4242 4242 4242
  - Test declined payment: 4000 0000 0000 0002
  - Test subscription flow
  - Test one-time flow
  - Verify webhooks (if configured)

- [ ] **Task 84**: Fix any bugs or issues found during testing
  - Document all bugs
  - Prioritize and fix
  - Re-test after fixes

- [ ] **Task 85**: **COMMIT**: Testing fixes and optimizations
  ```bash
  git add .
  git commit -m "fix: address testing issues and performance optimizations"
  ```

---

## Phase 11: Deployment (Tasks 86-95)

- [ ] **Task 86**: Merge develop into main for production release
  ```bash
  git checkout main
  git merge develop
  git tag -a v1.0.0 -m "Release v1.0.0 - AquaShine Pool Services MVP"
  ```

- [ ] **Task 87**: Create deployment configuration for Vercel
  - Create vercel.json with security headers
  - Configure build command for Next.js 16
  - Set framework to "nextjs"
  - Add X-Content-Type-Options, X-Frame-Options headers
  - Verify Turbopack compatibility
  - Set preferred region (iad1 for East Coast)

- [ ] **Task 88**: Set up environment variables in Vercel dashboard
  - NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY (test or live)
  - STRIPE_SECRET_KEY (test or live)
  - NEXT_PUBLIC_BASE_URL (production URL)

- [ ] **Task 89**: Deploy to Vercel and verify production build
  ```bash
  # Install Vercel CLI if needed
  npm i -g vercel

  # Deploy
  vercel --prod
  ```

- [ ] **Task 90**: Test production deployment end-to-end
  - Visit all pages
  - Test navigation
  - Test forms
  - Test Stripe checkout (use test mode initially)
  - Verify analytics (if configured)

- [ ] **Task 91**: Configure custom domain (if applicable)
  - Add domain in Vercel dashboard
  - Update DNS records
  - Verify SSL certificate
  - Update NEXT_PUBLIC_BASE_URL if needed

- [ ] **Task 92**: Create final production tag and release notes
  ```bash
  git tag -a v1.0.0-production -m "Production release"
  git push origin main --tags
  ```

---

## Quick Reference: Jump Points

**Start from scratch**: Task 1
**Already have Next.js setup**: Task 7 (Core Infrastructure)
**Have data/types ready**: Task 14 (Design System)
**Have UI components**: Task 22 (Layout)
**Layout done**: Task 29 (Home Page)
**Home page done**: Task 39 (Services Page)
**Services done**: Task 47 (Booking System)
**Booking done**: Task 59 (Contact Page)
**All pages done**: Task 74 (Testing)
**Testing done**: Task 86 (Deployment)

---

## Git Command Quick Reference

```bash
# View current branch
git branch

# View all branches
git branch -a

# Create and switch to new branch
git checkout -b feature/branch-name

# Switch to existing branch
git checkout branch-name

# Merge feature into develop
git checkout develop
git merge feature/branch-name

# View commit history
git log --oneline --graph --all

# View changes
git status
git diff

# Stage and commit
git add .
git commit -m "type: message"

# Push to remote
git push origin branch-name

# Pull latest changes
git pull origin develop
```

---

## Stripe Test Cards

```
Successful payment:        4242 4242 4242 4242
Declined:                  4000 0000 0000 0002
Requires authentication:   4000 0025 0000 3155
Insufficient funds:        4000 0000 0000 9995

Expiry: Any future date (e.g., 12/34)
CVC: Any 3 digits (e.g., 123)
ZIP: Any 5 digits (e.g., 12345)
```

---

## Completion Checklist

- [ ] All 8 services display correctly
- [ ] Navigation works on all devices
- [ ] Mobile menu functions properly
- [ ] Contact form validates correctly
- [ ] Stripe checkout works for subscriptions
- [ ] Stripe checkout works for one-time payments
- [ ] Success page displays after payment
- [ ] Canceled page displays on cancel
- [ ] Site is responsive 320px - 1440px+
- [ ] No horizontal scroll anywhere
- [ ] All links work
- [ ] Phone numbers are clickable
- [ ] Lighthouse scores 90+ on all metrics
- [ ] SEO metadata is complete
- [ ] Site deployed to production
- [ ] Custom domain configured (if applicable)

---

**Total Tasks: 92**
**Estimated Phases: 11**
**Commit Points: 11**

---

## 2026 Technology Improvements

### What's New vs 2024/2025 Stack

**Next.js 16.1** (was 14.x):
- ✅ Turbopack stable (5-10x faster dev, 2-5x faster builds)
- ✅ "use cache" directive for opt-in caching
- ✅ React 19 native support
- ✅ 20MB smaller install size
- ✅ File system caching for dev mode

**React 19.2** (was 18.x):
- ✅ `useOptimistic` hook for instant UI updates
- ✅ `useEffectEvent` for non-reactive effect logic
- ✅ Activity component for show/hide logic
- ✅ Server Components stable
- ✅ Better streaming and Suspense

**Tailwind CSS v4** (was 3.x):
- ✅ 5x faster full builds
- ✅ 100x faster incremental builds
- ✅ CSS-based configuration (no more JS config)
- ✅ Modern CSS features (cascade layers, @property, color-mix)
- ✅ Automatic content detection
- ✅ First-party Vite plugin

**Stripe API 2025-12-15** (was 2023-10-16):
- ✅ Latest API features
- ✅ Enhanced checkout customization
- ✅ Better subscription management
- ✅ Improved security features

**TypeScript 5.9** (was 5.0):
- ✅ Better type inference
- ✅ Performance improvements
- ✅ Enhanced strict mode checking

**Geist Font** (was Inter only):
- ✅ Vercel's optimized font
- ✅ Better rendering performance
- ✅ Professional appearance

### Performance Targets (2026)

```
Lighthouse Scores: 95+ (all categories)
First Contentful Paint: < 1.2s
Largest Contentful Paint: < 2.5s
Time to Interactive: < 2.5s
Cumulative Layout Shift: < 0.1
Total Blocking Time: < 200ms
Speed Index: < 3.0s
```

### Modern Patterns Used

1. **Server Components by Default**: All components are Server Components unless marked with 'use client'
2. **Streaming with Suspense**: Progressive page loading for better UX
3. **React 19 useOptimistic**: Instant UI feedback on user actions
4. **Edge Runtime Ready**: Components can run on edge with minimal changes
5. **Modern CSS**: Using cascade layers, container queries, and CSS variables
6. **Security-First**: Modern security headers, CSP, and best practices
7. **WCAG 2.2 AA**: Full accessibility compliance

---

## Resources & Documentation

### Official Docs
- [Next.js 16 Documentation](https://nextjs.org/blog/next-16)
- [React 19.2 Release](https://react.dev/blog/2025/10/01/react-19-2)
- [Tailwind CSS v4](https://tailwindcss.com/blog/tailwindcss-v4)
- [Stripe API 2025-12-15](https://docs.stripe.com/api/versioning)
- [TypeScript 5.9](https://devblogs.microsoft.com/typescript/)

### Key References
- [Turbopack Performance](https://nextjs.org/blog/next-16#turbopack-stable)
- [React 19 Features](https://react.dev/blog/2024/12/05/react-19)
- [Tailwind v4 Migration](https://tailwindcss.com/docs/upgrade-guide)
- [WCAG 2.2 Guidelines](https://www.w3.org/WAI/WCAG22/quickref/)
- [Core Web Vitals](https://web.dev/vitals/)

---

**Total Tasks: 92**
**Estimated Phases: 11**
**Commit Points: 11**
**Target Completion: Production-ready modern website**
