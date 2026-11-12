# Recreation Prompt: Denver Metro Luxury Real Estate Website

Build a premium luxury real estate website for the Denver metro market. Follow every specification below exactly.

---

## PART 1: TECH STACK & SETUP

Initialize a React + TypeScript + Vite project with Tailwind CSS v3.

**Install these dependencies:**
```bash
npm install lucide-react
```

**Configure `tailwind.config.js`:**
```js
export default {
  content: ['./index.html', './src/**/*.{js,ts,jsx,tsx}'],
  theme: {
    extend: {
      colors: {
        gold: { DEFAULT: '#B8860B', dark: '#8B6914' },
        dark: { DEFAULT: '#0a0a0a', lighter: '#6b6b6b' }
      },
      fontFamily: {
        display: ['"Playfair Display"', 'serif'],
        body: ['Inter', 'sans-serif'],
        mono: ['"JetBrains Mono"', 'monospace']
      }
    }
  },
  plugins: []
}
```

**Add to `index.html` head:**
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;500;600;700&family=Inter:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<meta name="description" content="Explore Denver luxury real estate, from Cherry Creek and Hilltop to Castle Pines and Boulder. Browse luxury homes, compare neighborhoods, and schedule a private tour.">
<meta name="keywords" content="Denver luxury real estate, Denver luxury homes, Denver mansions, Cherry Creek, Hilltop, Castle Pines, Boulder luxury homes">
<meta property="og:title" content="Denver Luxury Real Estate | Homes, Mansions & Elite Neighborhoods">
<meta property="og:description" content="Explore Denver luxury real estate, from Cherry Creek and Hilltop to Castle Pines and Boulder. Browse luxury homes, compare neighborhoods, and schedule a private tour.">
<title>Denver Luxury Real Estate | Homes, Mansions & Elite Neighborhoods</title>
```

**Add to `index.css`:**
```css
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  html { scroll-behavior: smooth; }
  body { font-family: 'Inter', sans-serif; color: #0a0a0a; background: #ffffff; }
  h1, h2, h3, h4, h5, h6 { font-family: 'Playfair Display', serif; }
}

@layer components {
  .gradient-text { background: linear-gradient(135deg, #B8860B 0%, #D4A84B 50%, #B8860B 100%); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; }
  .btn-primary { background: linear-gradient(135deg, #B8860B 0%, #D4A84B 100%); color: white; padding: 1rem 2.5rem; font-weight: 500; border-radius: 4px; transition: all 0.3s ease; }
  .btn-primary:hover { background: linear-gradient(135deg, #D4A84B 0%, #B8860B 100%); box-shadow: 0 4px 20px rgba(184,134,11,0.3); }
  .btn-outline { border: 2px solid #0a0a0a; color: #0a0a0a; padding: 1rem 2.5rem; font-weight: 500; border-radius: 4px; transition: all 0.3s ease; }
  .btn-outline:hover { background: #0a0a0a; color: white; }
  .btn-dark { background: #0a0a0a; color: white; padding: 0.75rem 1.5rem; font-weight: 500; border-radius: 4px; transition: all 0.3s ease; }
  .btn-dark:hover { background: #B8860B; }
  .link-underline { position: relative; }
  .link-underline::after { content: ''; position: absolute; bottom: -2px; left: 0; width: 0; height: 1px; background: #B8860B; transition: width 0.3s ease; }
  .link-underline:hover::after { width: 100%; }
  .community-card { border-radius: 8px; overflow: hidden; box-shadow: 0 1px 3px rgba(0,0,0,0.08); border: 1px solid #e5e5e5; background: white; transition: all 0.3s ease; }
  .community-card:hover { box-shadow: 0 8px 30px rgba(0,0,0,0.12); transform: translateY(-4px); }
  .property-card { border-radius: 8px; overflow: hidden; box-shadow: 0 1px 3px rgba(0,0,0,0.08); border: 1px solid #e5e5e5; background: white; transition: all 0.3s ease; }
  .property-card:hover { box-shadow: 0 8px 30px rgba(0,0,0,0.12); transform: translateY(-4px); }
}
```

---

## PART 2: SHARED COMPONENTS

### Navigation.tsx
Create a shared Navigation component used on ALL pages:
- Fixed position, z-50
- Transparent background initially, transitions to `bg-white/95 backdrop-blur-md shadow-sm` on scroll (trigger at scrollY > 100)
- Left: Logo link "Denver Metro **Luxury**" (Luxury in gold) + SSC & Company logo image below
- Center links (hidden on mobile): Communities, Listings, Market Insights, About, Contact — each smooth-scrolls to section ID
- Right: Phone button "(720) 663-0446" — gold bg when scrolled, white/10 border when transparent
- Mobile hamburger menu with slide-down panel
- Accepts `onNavigateHome?: () => void` prop for logo click

### Footer
- `bg-dark text-white` with gold top border (2px)
- 4 columns: Brand (logo + tagline), Quick Links, Resources, Contact
- Tagline: "Denver Metro Luxury | SSC & Company. Luxury real estate — Denver, CO. Cherry Creek, Hilltop, Cherry Hills Village, Castle Pines, Highlands Ranch, and 25+ metro communities. (720) 663-0446."
- Copyright: "© 2024 Denver Metro Luxury. All rights reserved."

---

## PART 3: HOME PAGE (App.tsx)

Build a single-page app with `currentView` state routing. Include ALL sections below on the home page.

### Section: Hero
- Full viewport height, `bg-dark` background with overlaid Denver skyline image at 40% opacity
- Content centered-left:
  - H1: "Denver luxury real estate" (white) + "**homes for sale from $1M to $25M**" (gold gradient)
  - Subtext: "Cherry Creek, Hilltop, Cherry Hills Village, Castle Pines, Boulder, and 30+ metro neighborhoods. Request a home valuation or search active listings now. Call Dan — (720) 663-0446."
  - Two CTAs: [Explore Communities] (gold btn) + [View Luxury Listings] (outline btn, white border)
- Animate content in on load with staggered delays

### Section: Quick Filters
- White background, 4 image cards in a row
- Cards: New Listings (green key icon), Price Reduced (trending-down icon), Open Houses (calendar icon), Recently Sold (checkmark icon)
- Each card has an image, icon overlay, and label

### Section: Communities (REORGANIZED INTO TWO GROUPS)

**Header:**
- Label: "NEIGHBORHOODS" (mono, gold, tracking)
- H2: "Signature Communities"
- Subtext: "Denver luxury homes by neighborhood — median prices, days on market, and active listings. Pick one below or call (720) 663-0446 for off-market inventory."
- Link: "View All 32 Denver Neighborhoods" → navigates to hub page

**Group 1: "Denver Core Luxury Neighborhoods" (H3 heading, centered)**
12 cards in 4-column grid:
1. Cherry Creek — Median $1.85M — Range $800K-$8M — DOM 28 — Tags: luxury retail, upscale dining
2. Hilltop — Median $2.80M — Range $1.5M-$12M — DOM 35 — Tags: estate living, top schools
3. Belcaro — Median $2.20M — Range $1.2M-$8M — DOM 32 — Tags: estate living, privacy
4. Washington Park — Median $1.45M — Range $700K-$5M — DOM 12 — Tags: outdoor lifestyle, historic homes
5. Washington Park West — Median $1.15M — Range $600K-$3.5M — DOM 14 — Tags: park access, walkable
6. Country Club — Median $1.95M — Range $900K-$6M — DOM 30 — Tags: historic homes, golf course
7. Bonnie Brae — Median $1.35M — Range $700K-$4M — DOM 18 — Tags: Tudor architecture, quiet streets
8. LoDo — Median $850K — Range $450K-$3.5M — DOM 18 — Tags: urban professionals, lock-and-leave
9. Sloan's Lake — Median $950K — Range $550K-$3.2M — DOM 16 — Tags: lake access, waterfront
10. Berkeley — Median $825K — Range $450K-$2.8M — DOM 12 — Tags: trendy dining, local shops
11. Highlands — Median $1.05M — Range $550K-$3.5M — DOM 14 — Tags: historic homes, city views
12. Observatory Park — Median $875K — Range $500K-$2.5M — DOM 15 — Tags: family-friendly, park access

**Group 2: "Suburban Luxury Markets" (H3 heading, centered)**
10 cards in 4-column grid:
1. Greenwood Village — Median $1.65M — Range $900K-$6M — DOM 28
2. Cherry Hills Village — Median $4.50M — Range $2M-$25M — DOM 45
3. Castle Pines — Median $1.85M — Range $950K-$6M — DOM 35
4. Highlands Ranch — Median $875K — Range $550K-$2.5M — DOM 22
5. Parker — Median $785K — Range $500K-$2M — DOM 25
6. Littleton — Median $725K — Range $450K-$1.8M — DOM 18
7. Golden — Median $925K — Range $600K-$3M — DOM 28
8. Evergreen — Median $850K — Range $500K-$2.5M — DOM 32
9. Lakewood — Median $675K — Range $400K-$1.6M — DOM 16
10. Boulder — Median $1.95M — Range $900K-$8M — DOM 32

Each card: image, median price overlay, name, description, price range with DollarSign icon, DOM with Clock icon, tags, "View Community Guide" button.

### Section: Featured Properties
- H2: "Featured Properties"
- Subtext: "Denver luxury listings — updated daily from MLS. Price, beds, sqft, and neighborhood for each home. Want pocket listings not shown here? Call (720) 663-0446."
- 3 property cards with image, price, address, bed/bath/sqft icons
- CTA: "View All Listings" (outline button)

### Section: Market Intelligence
- H2: "Denver Metro Market Insights"
- Subtext: "Denver luxury market data — live. Median prices, inventory, and days on market by neighborhood. Free quarterly reports. No email required."
- Two toggle buttons: "Price Trends" / "Inventory"
- Active state shows an iframe embed (use a placeholder div with chart styling)

### Section: Guides (Buyer + Seller)
- H2: "Your Guide to Success"
- Subtext: "Denver luxury real estate guidance — block by block. Neighborhood comps, honest pricing, and vetted lenders. One call to start. (720) 663-0446."
- Two cards side by side:
  - **Buyer's Guide**: "Buying a luxury home in Denver? Get pre-approved, tour 3–5 neighborhoods, submit a clean offer. We handle negotiation and contracts. Download the free buyer checklist or call (720) 663-0446." + 4 numbered steps + "Download the checklist" button
  - **Seller's Guide**: "Selling a luxury home in Denver? Free home valuation and pre-listing prep plan. Professional staging, photography, and targeted digital marketing included. Request your CMA — (720) 663-0446." + 4 numbered steps + "Request a valuation" button

### Section: Lifestyle
- Split layout: image left, content right
- H2: "Lifestyle, not just location"
- Text: "Denver lifestyle: 300+ days of sun, ski resorts 90 minutes west, James Beard-level dining in every direction. Search homes by lifestyle — walkable urban, golf course, mountain view, or acreage."
- 4 icon features: Dining, Outdoor Recreation, Culture, Architecture

### Section: Agent (Dan Navarro)
- Split layout: image left, content right
- Label: "Principal Broker & Founder" (gold)
- H2: "Dan Navarro"
- Bio: "Dan Navarro — Denver luxury real estate agent. Principal broker, SSC & Company / REALM member. 20+ years selling $1M–$25M homes in Cherry Creek, Hilltop, Cherry Hills, Wash Park, and Castle Pines. Call direct: (720) 663-0446."
- 3 stat boxes: 20+ Years, $2.5B+ Sold, 500+ Families
- Contact row: Phone (720) 663-0446, Email Dan@SSCandCompany.com, Schedule Consultation button

### Section: Contact
- H2: "Talk to Dan Today"
- Subtext: "Buying, selling, or need a home valuation. Same-day response. Call (720) 663-0446, email Dan@SSCandCompany.com, or fill out the form below."
- 2-column layout: contact info left, form right
- Form fields: Name, Email, Phone, Interest (dropdown: Buying/Selling/Both), Message (textarea)
- Submit button: "Send Message"

### Section: FAQ
- H2: "Denver Luxury Real Estate FAQs"
- Subtext: "Denver luxury real estate — common questions answered. Can't find yours? Call (720) 663-0446."
- 4 accordion items with ChevronDown toggle:

**Q1:** "What defines luxury real estate in Denver?"
**A1:** "Luxury homes in Denver start around $1M. What separates them: location, lot size, privacy, architecture, and finishes. Cherry Creek, Hilltop, and Cherry Hills set the standard."

**Q2:** "Where do wealthy buyers live in Denver?"
**A2:** "Cherry Creek, Hilltop, Cherry Hills Village, Country Club, Greenwood Village, Castle Pines, Wash Park, Boulder, and Golden foothills. Price ranges from $1M to $25M depending on the neighborhood."

**Q3:** "What are the best luxury neighborhoods in Denver Metro?"
**A3:** "Depends on what you want. Urban walkability — Cherry Creek or LoDo. Estates and privacy — Cherry Hills or Hilltop. Golf and gated — Castle Pines. Family-focused — Greenwood Village or Highlands Ranch. Call to narrow it down."

**Q4:** "Are there modern luxury homes in Denver?"
**A4:** "Yes. New construction and modern-design luxury homes are active in Cherry Creek, Sloan's Lake, Hilltop, Central Park, and LoHi. Browse current modern listings or call for off-market options."

- Include FAQPage schema JSON-LD in a `<script type="application/ld+json">` tag
- CTA: "More questions? Call Dan — (720) 663-0446. Same-day response." + button

---

## PART 4: INDIVIDUAL COMMUNITY/NEIGHBORHOOD PAGES

Create 12 separate page components. Each follows this EXACT template:

```tsx
import { useEffect, useRef, useState } from 'react';
import { ArrowRight, MapPin, Bed, Bath, Maximize, Phone, Mail, ChevronDown } from 'lucide-react';
import Navigation from '../components/Navigation';

interface PageProps { onBack: () => void; }

export default function PageName({ onBack }: PageProps) {
  useEffect(() => window.scrollTo(0, 0), []);
  const sectionRef = useRef<HTMLElement>(null);
  const [visible, setVisible] = useState(true);
  const [openIndex, setOpenIndex] = useState<number | null>(0);
  // IntersectionObserver setup...
  
  // FAQ array (4 questions specific to this community)
  // FAQ schema JSON-LD
  // Sample listings (3)
  // Community/neighborhood data object
  
  return (
    <div className="min-h-screen bg-white">
      <script type="application/ld+json" dangerouslySetInnerHTML={{ __html: JSON.stringify(faqSchema) }} />
      <Navigation onNavigateHome={onBack} />
      
      {/* Hero: full-width image with gradient overlay, community name, tagline */}
      {/* Stats bar: 4 columns — Median Price, Price Range, DOM, Lifestyle */}
      {/* Main content: 2/3 description + 1/3 sticky sidebar */}
      {/* FAQ section */}
      {/* Featured Listings: 3 cards */}
      {/* Dark CTA section with phone number */}
    </div>
  );
}
```

Each page has: Hero image → Stats bar → About section (2 paragraphs) → Features list → Nearby attractions → Sticky sidebar (call/email buttons, tags) → FAQ accordion (4 questions) → Sample listings → Dark CTA.

### SEO Community Pages (6):

**1. HighlandsRanchPage.tsx**
- H1: "Highlands Ranch Luxury Homes"
- Tagline: "Space, amenities, and suburban luxury in the South Metro"
- Median: $875K | Range: $550K-$2.5M | DOM: 22 | Lifestyle: Family Executive
- FAQs: Is Highlands Ranch a luxury market? / Who buys luxury homes here? / What types of luxury homes? / How does it compare with Castle Pines?

**2. CastlePinesPage.tsx**
- H1: "Castle Pines Luxury Homes"
- Tagline: "Gated luxury with championship golf and panoramic views"
- Median: $1.85M | Range: $950K-$6M | DOM: 35 | Lifestyle: Golf & Nature

**3. LoneTreePage.tsx**
- H1: "Lone Tree Luxury Homes"
- Tagline: "Polished luxury with DTC convenience and newer housing"
- Median: $925K | Range: $650K-$2.2M | DOM: 18 | Lifestyle: Executive Convenience

**4. ParkerPage.tsx**
- H1: "Parker Luxury Homes"
- Tagline: "Spacious luxury living with room to grow south of Denver"
- Median: $785K | Range: $500K-$2M | DOM: 25 | Lifestyle: Space & Family

**5. BoulderPage.tsx**
- H1: "Boulder Luxury Homes"
- Tagline: "Premium Front Range living with mountain views and lifestyle prestige"
- Median: $1.95M | Range: $900K-$8M | DOM: 32 | Lifestyle: Mountain Lifestyle

**6. LouisvilleSuperiorPage.tsx**
- H1: "Louisville & Superior Luxury Homes"
- Tagline: "Boulder-adjacent luxury with strong schools and convenience"
- Median: $925K | Range: $650K-$2M | DOM: 20 | Lifestyle: Boulder-Adjacent

### SEO Neighborhood Pages (6):

**7. CentralParkPage.tsx**
- H1: "Central Park Luxury Homes"
- Tagline: "Modern Denver living with parks, planning, and convenience"
- Median: $785K | Range: $550K-$1.8M | DOM: 15 | Lifestyle: Modern Family

**8. LoDoHighlandPage.tsx**
- H1: "LoDo & Highland Luxury Homes"
- Tagline: "Urban luxury with walkability, architecture, and city energy"
- Median: $875K | Range: $500K-$3.5M | DOM: 18 | Lifestyle: Urban Luxury

**9. CapitolHillPage.tsx**
- H1: "Capitol Hill Luxury Condos & Homes"
- Tagline: "Historic character meets cultural proximity in central Denver"
- Median: $625K | Range: $350K-$1.8M | DOM: 20 | Lifestyle: Historic Urban

**10. ArvadaLuxuryPage.tsx**
- H1: "Arvada Luxury Homes"
- Tagline: "West-metro luxury with foothills access and suburban comfort"
- Median: $725K | Range: $450K-$1.8M | DOM: 18 | Lifestyle: West Metro Suburban

**11. GoldenLakewoodFoothillsPage.tsx**
- H1: "Golden & Lakewood Foothills Luxury Homes"
- Tagline: "Privacy, views, and mountain lifestyle within reach of Denver"
- Median: $925K | Range: $600K-$3M | DOM: 28 | Lifestyle: Foothills Living

**12. DTCCorridorPage.tsx**
- H1: "DTC Corridor Luxury Homes"
- Tagline: "Executive convenience with refined South Metro living"
- Median: $825K | Range: $550K-$2.2M | DOM: 20 | Lifestyle: Executive Convenience

---

## PART 5: ROUTING

In App.tsx, use state-based routing:
```tsx
const [currentView, setCurrentView] = useState<'home' | 'highlands-ranch' | 'castle-pines' | ...>('home');
```

When a community card is clicked, check the ID and render the matching page component. All 12 SEO pages + generic CommunityPage for other IDs.

Render the shared Navigation on home view. Pass `onBack={handleBackToHome}` to all page components.

---

## PART 6: CONTENT RULES

1. **Phone number** (720) 663-0446 appears in EVERY section
2. **Email**: Dan@SSCandCompany.com
3. **Agent**: Dan Navarro, Principal Broker, SSC & Company / REALM member
4. **CTA tone**: Direct, action-oriented, always offers a phone call
5. **SEO**: Include neighborhood names + price ranges naturally in copy
6. **FAQs**: Each page has 4 unique FAQs + FAQPage schema JSON-LD
7. **Images**: Use `/images/community_[name].jpg` pattern. Generate images with AI for each community/neighborhood hero and featured property.

---

## PART 7: IMAGES TO GENERATE

Generate the following images using AI image generation:
- `/images/community_cherry_creek.jpg` — Cherry Creek neighborhood
- `/images/community_hilltop.jpg` — Hilltop luxury estates
- `/images/community_belcaro.jpg` — Belcaro neighborhood
- `/images/community_wash_park.jpg` — Washington Park
- `/images/community_lodo.jpg` — Downtown LoDo
- `/images/community_sloans_lake.jpg` — Sloan's Lake waterfront
- `/images/community_greenwood.jpg` — Greenwood Village
- `/images/community_cherry_hills.jpg` — Cherry Hills Village estates
- `/images/community_castle_pines.jpg` — Castle Pines golf community
- `/images/community_highlands_ranch.jpg` — Highlands Ranch
- `/images/community_parker.jpg` — Parker Colorado
- `/images/community_boulder.jpg` — Boulder with Flatirons
- `/images/agent_dan.jpg` — Professional headshot of male real estate agent
- `/images/property_1.jpg` through `/images/property_3.jpg` — Luxury homes
- `/images/lifestyle_dining.jpg` — Upscale Denver dining
- `/images/lifestyle_outdoor.jpg` — Colorado outdoor recreation
- `/images/lifestyle_culture.jpg` — Denver cultural scene
- `/images/lifestyle_architecture.jpg` — Modern Denver architecture
- `/images/hero_denver.jpg` — Denver skyline at golden hour
- `/images/ssc_logo.png` — SSC & Company logo

---

## FINAL OUTPUT
Build the complete website with all 12+ pages, home page sections, shared navigation, FAQ schema, SEO copy, and goal-completion CTAs throughout. Deploy as a static site.
