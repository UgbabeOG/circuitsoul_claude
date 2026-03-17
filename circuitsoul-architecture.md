# CircuitSoul Ltd — Next.js + TypeScript + Tailwind Architecture

## Project Stack
- **Framework**: Next.js 14 (App Router)
- **Language**: TypeScript 5
- **Styling**: Tailwind CSS v3 + CSS Variables
- **Animation**: Framer Motion
- **Icons**: Lucide React
- **State**: Zustand (client) + React Server Components (server)
- **Forms**: React Hook Form + Zod
- **Fonts**: next/font (Cabinet Grotesk, Geist Mono, Instrument Sans)
- **SEO**: Next.js Metadata API + JSON-LD
- **Deployment**: Vercel

---

## Folder Structure

```
circuitsoul/
├── app/
│   ├── layout.tsx                  # Root layout: Nav, Footer, cursor, toast
│   ├── page.tsx                    # Home page (/)
│   ├── products/
│   │   └── page.tsx                # Products page (/products)
│   ├── services/
│   │   └── page.tsx                # Services page (/services)
│   ├── connect/
│   │   └── page.tsx                # Connect page (/connect)
│   ├── blog/
│   │   ├── page.tsx                # Blog listing (/blog)
│   │   └── [slug]/
│   │       └── page.tsx            # Blog post (/blog/[slug])
│   ├── about/
│   │   └── page.tsx                # About page (/about)
│   ├── contact/
│   │   └── page.tsx                # Contact page (/contact)
│   ├── globals.css                 # Design tokens, base styles
│   └── not-found.tsx               # 404 page
│
├── components/
│   ├── layout/
│   │   ├── Navbar.tsx              # Fixed nav with scroll state
│   │   ├── Footer.tsx              # Footer with column links
│   │   ├── MobileMenu.tsx          # Mobile drawer nav
│   │   └── Cursor.tsx              # Custom cursor (client component)
│   │
│   ├── home/
│   │   ├── Hero.tsx                # Hero section with dashboard
│   │   ├── HeroDashboard.tsx       # Floating Shield dashboard widget
│   │   ├── Ticker.tsx              # Animated metrics ticker/marquee
│   │   ├── BentoGrid.tsx           # 12-col bento layout wrapper
│   │   ├── PlatformCard.tsx        # Shield / CloudOps / Flow card
│   │   ├── ConnectTeaser.tsx       # Connect coming-soon bento card
│   │   ├── EcosystemGrid.tsx       # 10-cell service grid
│   │   ├── IndustriesRow.tsx       # Scrolling industry pills
│   │   ├── FAQSection.tsx          # Accordion FAQ
│   │   └── CTABand.tsx             # Full-width CTA section
│   │
│   ├── products/
│   │   ├── ProductHero.tsx         # Products page hero
│   │   ├── ProductTabs.tsx         # Shield / CloudOps / Flow tabs
│   │   ├── ProductDetail.tsx       # Product detail layout (problem/features/dashboard)
│   │   ├── ShieldDashboard.tsx     # Shield mock dashboard
│   │   ├── CloudOpsDashboard.tsx   # CloudOps mock dashboard
│   │   └── FlowDashboard.tsx       # Flow mock dashboard
│   │
│   ├── services/
│   │   ├── ServicesHero.tsx        # Services page hero
│   │   └── ServiceCard.tsx         # Individual service card
│   │
│   ├── connect/
│   │   ├── ConnectHero.tsx         # Connect page hero + waitlist
│   │   ├── WaitlistForm.tsx        # Email capture form
│   │   └── HowItWorks.tsx          # 4-step how-it-works grid
│   │
│   ├── blog/
│   │   ├── BlogGrid.tsx            # Blog card grid
│   │   ├── BlogCard.tsx            # Individual blog card
│   │   └── NewsletterStrip.tsx     # Email subscription strip
│   │
│   ├── about/
│   │   ├── AboutSplit.tsx          # Mission + profile card split
│   │   ├── ValuesGrid.tsx          # 4-value card grid
│   │   └── MetricsRow.tsx          # 4-metric stat row
│   │
│   ├── contact/
│   │   ├── ContactGrid.tsx         # Info + form split layout
│   │   ├── ContactInfoBlock.tsx    # Individual contact info row
│   │   └── ContactForm.tsx         # Multi-field contact form
│   │
│   └── ui/
│       ├── Button.tsx              # btn-solid / btn-wire / btn-volt variants
│       ├── Eyebrow.tsx             # Section label chip
│       ├── Chip.tsx                # Feature tag chip (arc/volt/pur/amb)
│       ├── SectionLabel.tsx        # Reusable eyebrow + title + desc
│       ├── ScrollReveal.tsx        # IntersectionObserver reveal wrapper
│       ├── Toast.tsx               # Toast notification
│       ├── SparklineChart.tsx      # Animated bar sparkline
│       ├── ShieldOrb.tsx           # Animated ring orbital SVG
│       ├── FlowPipeline.tsx        # Step → Step → pipeline display
│       ├── DashTile.tsx            # Dashboard metric tile
│       ├── DashLog.tsx             # Dashboard event log row
│       └── Modal.tsx               # Generic modal (for demo booking)
│
├── lib/
│   ├── constants.ts                # Nav links, platform data, service data
│   ├── blog.ts                     # Blog post data / MDX loader
│   ├── analytics.ts                # Posthog / Plausible setup
│   └── schemas.ts                  # Zod schemas for forms
│
├── hooks/
│   ├── useScrolled.ts              # Navbar scroll state
│   ├── useReveal.ts                # IntersectionObserver hook
│   ├── useCursor.ts                # Custom cursor position hook
│   └── useToast.ts                 # Toast state management
│
├── types/
│   ├── platform.ts                 # Platform product types
│   ├── service.ts                  # Service/ecosystem types
│   └── blog.ts                     # Blog post types
│
├── public/
│   ├── og-image.png                # Open Graph image
│   ├── favicon.ico
│   └── logos/
│
├── styles/
│   └── tokens.css                  # CSS custom properties (design tokens)
│
├── next.config.ts
├── tailwind.config.ts
└── tsconfig.json
```

---

## Core Component Examples

### `components/ui/Button.tsx`
```tsx
import { type ButtonHTMLAttributes, forwardRef } from 'react'
import { cn } from '@/lib/utils'

type Variant = 'solid' | 'wire' | 'volt'
type Size = 'sm' | 'md' | 'lg'

interface ButtonProps extends ButtonHTMLAttributes<HTMLButtonElement> {
  variant?: Variant
  size?: Size
  loading?: boolean
}

const variantClasses: Record<Variant, string> = {
  solid: 'bg-arc text-white hover:bg-arc-2 hover:-translate-y-px shadow-arc-glow',
  wire:  'bg-transparent border border-rim-2 text-text-2 hover:border-arc-2 hover:text-text',
  volt:  'bg-transparent border border-volt text-volt hover:bg-volt-glow hover:-translate-y-px',
}

const sizeClasses: Record<Size, string> = {
  sm: 'px-4 py-2 text-sm rounded-lg gap-1.5',
  md: 'px-5 py-2.5 text-sm rounded-lg gap-2',
  lg: 'px-7 py-3.5 text-base rounded-xl gap-2',
}

export const Button = forwardRef<HTMLButtonElement, ButtonProps>(
  ({ variant = 'solid', size = 'md', loading, className, children, ...props }, ref) => (
    <button
      ref={ref}
      className={cn(
        'inline-flex items-center font-medium transition-all duration-200',
        'font-body tracking-[0.01em] cursor-pointer',
        variantClasses[variant],
        sizeClasses[size],
        loading && 'opacity-70 cursor-wait',
        className
      )}
      disabled={loading}
      {...props}
    >
      {loading ? <span className="animate-spin mr-1.5">⟳</span> : null}
      {children}
    </button>
  )
)
Button.displayName = 'Button'
```

### `components/ui/ScrollReveal.tsx`
```tsx
'use client'
import { useEffect, useRef, type ReactNode } from 'react'
import { motion, useInView, useAnimation } from 'framer-motion'

interface ScrollRevealProps {
  children: ReactNode
  delay?: number
  className?: string
}

export function ScrollReveal({ children, delay = 0, className }: ScrollRevealProps) {
  const ref = useRef<HTMLDivElement>(null)
  const isInView = useInView(ref, { once: true, margin: '0px 0px -60px 0px' })
  const controls = useAnimation()

  useEffect(() => {
    if (isInView) {
      controls.start({ opacity: 1, y: 0, transition: { duration: 0.65, delay, ease: [0.4, 0, 0.2, 1] }})
    }
  }, [isInView, controls, delay])

  return (
    <motion.div ref={ref} initial={{ opacity: 0, y: 28 }} animate={controls} className={className}>
      {children}
    </motion.div>
  )
}
```

### `components/home/BentoGrid.tsx`
```tsx
import { PlatformCard } from './PlatformCard'
import { ConnectTeaser } from './ConnectTeaser'
import { platforms } from '@/lib/constants'

export function BentoGrid() {
  return (
    <div className="grid grid-cols-12 gap-[1.1rem]">
      {/* Shield — 7 cols wide */}
      <div className="col-span-12 lg:col-span-7">
        <PlatformCard platform={platforms.shield} variant="wide" />
      </div>
      {/* CloudOps — 5 cols */}
      <div className="col-span-12 lg:col-span-5">
        <PlatformCard platform={platforms.cloudops} variant="tall" />
      </div>
      {/* Flow — 6 cols */}
      <div className="col-span-12 lg:col-span-6">
        <PlatformCard platform={platforms.flow} variant="half" />
      </div>
      {/* Connect — 6 cols */}
      <div className="col-span-12 lg:col-span-6">
        <ConnectTeaser />
      </div>
    </div>
  )
}
```

### `lib/constants.ts`
```ts
export const platforms = {
  shield: {
    id: 'shield',
    name: 'CircuitSoul Shield',
    tagline: 'AI-Driven Cybersecurity & Compliance Platform',
    description: 'Enterprise-grade security intelligence for startups without dedicated security teams.',
    icon: '🛡',
    color: 'arc' as const,
    chips: ['Threat Detection', 'NDPR Compliance', 'Vulnerability Scanning', 'Risk Dashboards'],
    href: '/products?tab=shield',
  },
  cloudops: {
    id: 'cloudops',
    name: 'CircuitSoul CloudOps',
    tagline: 'Cloud Infrastructure & DevSecOps Platform',
    description: 'Manage, optimize, and scale your cloud environment with security-first automation.',
    icon: '☁',
    color: 'purple' as const,
    chips: ['Cost Optimization', 'DevOps Pipelines', 'Multi-Cloud Monitoring'],
    href: '/products?tab=cloudops',
  },
  flow: {
    id: 'flow',
    name: 'CircuitSoul Flow',
    tagline: 'Workflow Automation & Internal Tools',
    description: 'Automate operations, build internal dashboards, and connect your systems.',
    icon: '⚡',
    color: 'volt' as const,
    chips: ['Process Automation', 'System Integrations', 'Analytics'],
    href: '/products?tab=flow',
  },
} as const

export const services = [
  { id: 'ai-agents', name: 'AI Agents Development', icon: '🤖', color: 'arc' },
  { id: 'consulting', name: 'Technology Consulting', icon: '🔭', color: 'purple' },
  { id: 'cloud-migration', name: 'Cloud Migration', icon: '☁', color: 'purple' },
  { id: 'web-dev', name: 'Custom Web Development', icon: '💻', color: 'arc' },
  { id: 'mobile-dev', name: 'Mobile App Development', icon: '📱', color: 'arc' },
  { id: 'software-eng', name: 'Custom Software Engineering', icon: '⚙', color: 'volt' },
  { id: 'cybersecurity', name: 'Cybersecurity Consulting', icon: '🔒', color: 'arc' },
  { id: 'ui-ux', name: 'UI/UX Design', icon: '🎨', color: 'volt' },
  { id: 'it-support', name: 'IT Support Services', icon: '🛠', color: 'amber' },
  { id: 'hardware', name: 'Hardware Procurement', icon: '🖥', color: 'amber' },
  { id: 'training', name: 'Technology Training', icon: '🎓', color: 'purple' },
] as const

export const navLinks = [
  { label: 'Home', href: '/' },
  { label: 'Products', href: '/products' },
  { label: 'Services', href: '/services' },
  { label: 'Connect', href: '/connect' },
  { label: 'Blog', href: '/blog' },
  { label: 'About', href: '/about' },
  { label: 'Contact', href: '/contact' },
] as const
```

### `app/layout.tsx`
```tsx
import type { Metadata } from 'next'
import { Cabinet_Grotesk, Geist_Mono } from 'next/font/google'
import { Navbar } from '@/components/layout/Navbar'
import { Footer } from '@/components/layout/Footer'
import { Cursor } from '@/components/layout/Cursor'
import { Toast } from '@/components/ui/Toast'
import './globals.css'

const display = Cabinet_Grotesk({ subsets: ['latin'], weight: ['400','500','700','800','900'], variable: '--font-display' })
const mono = Geist_Mono({ subsets: ['latin'], weight: ['300','400','500'], variable: '--font-mono' })

export const metadata: Metadata = {
  title: { default: 'CircuitSoul — Digital Infrastructure for Africa', template: '%s | CircuitSoul' },
  description: 'CircuitSoul builds enterprise-grade cybersecurity, cloud infrastructure, and automation platforms engineered for African startups and SMEs.',
  keywords: ['cybersecurity Africa', 'cloud infrastructure Nigeria', 'SaaS Africa', 'DevOps Nigeria'],
  openGraph: { title: 'CircuitSoul — Digital Backbone for Africa\'s Startups', type: 'website', locale: 'en_NG' },
  robots: { index: true, follow: true },
}

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en" className={`${display.variable} ${mono.variable}`}>
      <body>
        <Cursor />
        <Navbar />
        <main>{children}</main>
        <Footer />
        <Toast />
      </body>
    </html>
  )
}
```

### `tailwind.config.ts`
```ts
import type { Config } from 'tailwindcss'

const config: Config = {
  content: ['./app/**/*.{ts,tsx}', './components/**/*.{ts,tsx}'],
  theme: {
    extend: {
      colors: {
        ink: { DEFAULT: '#03080f', 2: '#060e1c', 3: '#0a1628', 4: '#0e1e3a', 5: '#162447' },
        arc: { DEFAULT: '#1557ff', 2: '#3d78ff', 3: '#6699ff', glow: 'rgba(21,87,255,0.22)' },
        volt: { DEFAULT: '#00f2a0', 2: '#00d488', glow: 'rgba(0,242,160,0.15)' },
        rim: { DEFAULT: 'rgba(255,255,255,0.07)', 2: 'rgba(255,255,255,0.13)', 3: 'rgba(255,255,255,0.22)' },
        text: { DEFAULT: '#dde8f8', 2: '#8fa8cc', 3: '#4d6585', 4: '#2a3d55' },
      },
      fontFamily: {
        display: ['var(--font-display)', 'sans-serif'],
        mono: ['var(--font-mono)', 'monospace'],
        body: ['Instrument Sans', 'sans-serif'],
      },
      animation: {
        'rot': 'rotate 20s linear infinite',
        'blip': 'blip 2s ease-in-out infinite',
        'float': 'float 8s ease-in-out infinite',
        'sheen': 'sheen 3s infinite 1s',
        'tick': 'ticker 35s linear infinite',
      },
    },
  },
  plugins: [],
}
export default config
```

### `types/platform.ts`
```ts
export type PlatformColor = 'arc' | 'purple' | 'volt' | 'amber'
export type PlatformVariant = 'wide' | 'tall' | 'half'

export interface Platform {
  id: string
  name: string
  tagline: string
  description: string
  icon: string
  color: PlatformColor
  chips: readonly string[]
  href: string
  problem?: string
  howItWorks?: string
  capabilities?: string[]
  targetUsers?: string[]
}

export interface DashboardMetric {
  label: string
  value: string | number
  change?: string
  direction?: 'up' | 'down' | 'neutral'
  color?: 'green' | 'blue' | 'amber'
}

export interface DashboardEvent {
  type: 'ok' | 'warn' | 'error'
  message: string
  time: string
}
```

---

## SEO Structure

### Per-page Metadata pattern
```tsx
// app/products/page.tsx
import type { Metadata } from 'next'

export const metadata: Metadata = {
  title: 'Platform Products — Shield, CloudOps, Flow',
  description: 'Explore CircuitSoul\'s three infrastructure platforms: Shield for cybersecurity, CloudOps for cloud management, and Flow for workflow automation.',
  openGraph: {
    title: 'CircuitSoul Platforms — Infrastructure for African Startups',
    description: 'Enterprise-grade cybersecurity, cloud operations, and automation platforms built for Africa.',
  },
}
```

### JSON-LD Structured Data (app/layout.tsx)
```tsx
const structuredData = {
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "CircuitSoul Ltd",
  "url": "https://circuitsoul.io",
  "logo": "https://circuitsoul.io/logo.png",
  "description": "Digital infrastructure platforms for African startups and SMEs",
  "foundingLocation": { "@type": "Place", "name": "Nigeria" },
  "areaServed": "Africa",
  "sameAs": ["https://linkedin.com/company/circuitsoul", "https://twitter.com/circuitsoul"],
  "offers": [
    { "@type": "SoftwareApplication", "name": "CircuitSoul Shield", "applicationCategory": "SecurityApplication" },
    { "@type": "SoftwareApplication", "name": "CircuitSoul CloudOps", "applicationCategory": "BusinessApplication" },
    { "@type": "SoftwareApplication", "name": "CircuitSoul Flow", "applicationCategory": "BusinessApplication" }
  ]
}
```

---

## Performance Notes

- All dashboard widgets use `'use client'` — rest is React Server Components
- `next/font` eliminates layout shift from font loading
- `ScrollReveal` uses `IntersectionObserver` — no layout jank
- Ticker/marquee uses CSS `transform` animation — GPU-accelerated
- Blog page uses Static Generation (`generateStaticParams`)
- Contact form submits to `/api/contact` Route Handler with Resend
- Images use `next/image` with `priority` on hero assets

---

## Environment Variables
```bash
# .env.local
RESEND_API_KEY=            # Email delivery
NEXT_PUBLIC_POSTHOG_KEY=   # Analytics
NEXT_PUBLIC_SITE_URL=https://circuitsoul.io
WAITLIST_WEBHOOK=          # Webhook for waitlist submissions
```
