# Vyper Studio — Development Standards

## Description
Use when creating any web project, page, section, or component 
for Vyper Studio. These rules apply automatically to every 
project without exception.

---

## 1. TECHNICAL STACK (NON-NEGOTIABLE)

- **Framework:** Vite + React SPA — NEVER TanStack Start, 
  NEVER Next.js, under any circumstance
- **Routing:** React Router DOM (multi-page projects only)
- **Styles:** Tailwind CSS
- **Package manager:** npm — NEVER bun, delete bun.lockb if present
- **Always include vercel.json at project root:**
```json
{ "rewrites": [{ "source": "/(.*)", "destination": "/index.html" }] }
```
- **State management:** React state (useState, useContext, useReducer)
  — NEVER localStorage, NEVER sessionStorage
- **Icons:** lucide-react (already installed, no extra dependencies)
- **Deployment:** Compatible with Vercel and Cloudflare Pages

---

## 2. IMAGES — CRITICAL RULES

**NEVER generate, create, or hallucinate images.**

When a section requires images, always use placehold.co with 
appropriate dimensions and colors matching the project palette:

```
https://placehold.co/[WIDTH]x[HEIGHT]/[BG_COLOR]/[TEXT_COLOR]
```

Examples by section type:
- Hero background: `placehold.co/1920x1080/0A0A0A/333333`
- Product card (portrait): `placehold.co/400x500/1A1A1A/444444`
- Team member (square): `placehold.co/400x400/1A1A1A/444444`
- Gallery image: `placehold.co/600x600/1A1A1A/333333`
- Event banner (wide): `placehold.co/800x400/1A1A1A/444444`
- Logo placeholder: `placehold.co/200x80/FFFFFF/333333`

Color the placeholder background close to the project's palette 
so the layout feels intentional, not broken.

Never use Unsplash, Pexels, AI-generated images, or random URLs.

---

## 3. HERO SECTIONS — SIZE AND PROPORTIONS

**Desktop heroes must NOT be full-screen unless explicitly requested.**

Default hero heights:
- Main hero (home page): `min-h-[70vh]` — never `100vh` on desktop
- Sub-page hero (interior pages): `py-24 md:py-32` — compact, 
  not full screen
- On mobile: heroes can be taller, `min-h-[80vh]` is acceptable

Hero content must be vertically centered and never feel empty. 
If there is too much empty space above or below the content, 
reduce padding — do not leave dead space.

---

## 4. MOBILE HAMBURGER MENU — FLEXIBLE BUT ALWAYS FUNCTIONAL

The hamburger menu style can vary per project aesthetic, 
but must ALWAYS meet these requirements:

**Non-negotiable behavior:**
- Drawer opens with smooth animation (0.3s ease-in-out)
- Background is 100% opaque — NEVER transparent or semi-transparent
- Dark overlay covers the rest of the screen (rgba(0,0,0,0.6) minimum)
- Clicking the overlay closes the menu
- `body` gets `overflow: hidden` while menu is open
- Smooth scroll to section when a nav link is tapped

**Style options (choose based on project):**

Option A — Slide from right (most common):
```css
transform: translateX(100%) → translateX(0)
width: 80vw, height: 100vh
```

Option B — Full screen overlay (elegant/premium):
```css
opacity: 0 → 1, scale: 0.98 → 1
width: 100vw, height: 100vh
```

Option C — Slide from left (less common):
```css
transform: translateX(-100%) → translateX(0)
width: 75vw, height: 100vh
```

**Links animation:** always cascade with 0.05s delay between each link
(translateX or translateY + opacity, depending on the style chosen)

**Reference for a clean minimal hamburger:** 
The Dr. Alejandro Vargas demo uses a simple, elegant approach — 
white background drawer with black text, subtle shadow, 
clean typography. Use this style for professional/personal sites.

---

## 5. ANIMATIONS — GLOBAL RULES

All animations must be fluid, intentional, and never jarring.

**Intersection Observer (scroll reveal):**
- Default: `opacity: 0 → 1` + `translateY(20px) → translateY(0)`
- Duration: 0.5s ease-out
- Stagger between cards/items: 0.08s delay increment
- Trigger threshold: 0.12 (element 12% visible before animating)
- Always use `once: true` — animate only the first time

**Hover effects on cards:**
- Elevation: `translateY(-4px)` to `-6px`
- Duration: 0.25s ease
- Add subtle shadow increase
- Optional border highlight matching accent color

**Page transitions (multi-page):**
- Fade: `opacity: 0 → 1` in 0.2s
- Optionally add `scale: 0.98 → 1`

**Loading states:**
- Use skeleton screens (gray animated blocks) not spinners
- Match skeleton color to project background

**What NOT to do:**
- No bouncing, no elastic, no excessive spring animations
- No animations that repeat infinitely and distract the user
- No animations longer than 0.8s for UI elements
- No CSS `animation: spin` on anything other than a loader

---

## 6. NAVIGATION — DESKTOP AND MOBILE

**Desktop navbar:**
- Fixed position, stays visible on scroll
- Changes background on scroll (transparent → solid color + shadow)
- Smooth scroll to section anchors
- Active link indicator (underline or color change)
- CTA button aligned to the right

**Mobile navbar:**
- Logo on the left, hamburger icon on the right
- Social media icons (if any) should be inside the drawer, 
  not crowding the top bar
- Drawer includes CTA button at the bottom, prominently styled

---

## 7. TYPOGRAPHY — CONSISTENCY RULES

- Use Google Fonts, always load via `<link>` in index.html
- Maximum 2 font families per project (1 serif + 1 sans-serif, 
  or 2 sans-serif with different weights)
- Title hierarchy must be visually clear: 
  h1 much larger than h2, h2 clearly larger than h3
- Body text minimum: 16px (1rem), line-height: 1.6–1.8
- Never use font-size below 12px for any visible text
- Letter-spacing for uppercase labels: 0.1em to 0.2em

**Avoid:**
- More than 3 different font sizes in the same section
- Mixing too many font weights (pick 2-3 max)

---

## 8. LAYOUT AND SPACING

**Section padding (consistent across all sections):**
- Mobile: `py-16 px-4` (64px top/bottom, 16px sides)
- Desktop: `py-24 px-8` or `py-32 px-16` (96–128px top/bottom)

**Max content width:**
- Always wrap content in a max-width container: `max-w-6xl mx-auto`
- For text-heavy sections: `max-w-3xl mx-auto`
- Never let text span full viewport width on desktop

**Grid layouts:**
- Cards: `grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6`
- Two-column sections: `grid-cols-1 md:grid-cols-2 gap-12`
- Always define gap — never rely on margin alone

**Avoid dead space:**
- If a section feels empty, add a subtle decorative element, 
  a divider, or reduce the padding
- Sections should feel dense and purposeful, not spacious and empty

---

## 9. SUPABASE INTEGRATION

**Connection order (CRITICAL):**
Connect Supabase in Lovable settings BEFORE sending any prompt. 
If connected after, Lovable may use its own internal backend.

**Authentication:**
- Always use `supabase.auth.signInWithPassword()`
- Always use `supabase.auth.signOut()`
- Protect admin routes: check `supabase.auth.getSession()` 
  on mount, redirect to login if not authenticated
- Never hardcode credentials in frontend code

**Data fetching:**
- Always handle loading states with skeleton screens
- Always handle empty states with a meaningful message
- Always handle errors gracefully (show user-friendly message)

**Storage (images):**
- Images in cards: always use `object-contain` not `object-cover` 
  to prevent unwanted cropping
- Aspect ratio containers: use `aspect-[4/5]` for portrait, 
  `aspect-[16/9]` for landscape, `aspect-square` for square
- Public bucket: generate URLs with `supabase.storage.from('bucket').getPublicUrl('path')`

**Admin panel (/admin):**
- NO visible link in navbar or footer — access only by typing URL
- Login page at `/admin` or `/admin/login`
- After login, redirect to `/admin/dashboard` or `/admin/panel`
- Always include logout button inside the panel

---

## 10. FORMS

**Behavior:**
- All required fields must have visible validation
- Show inline error messages below each field (not alerts)
- Success state: replace form with a confirmation message 
  or show a toast notification
- Button text changes while submitting: 
  "Enviar" → "Enviando..." → "¡Enviado!"
- Disable submit button while request is in progress

**Styling:**
- Focus state: border color changes to accent color + subtle glow
- Error state: border turns red, error message in red below
- Input height: at least 44px (touch-friendly on mobile)
- Textarea: minimum 120px height, resize: vertical

**WhatsApp forms (no backend):**
- Build the message string from form fields
- Use `encodeURIComponent()` on the message
- Open: `https://wa.me/[NUMBER]?text=[ENCODED_MESSAGE]`
- Open in new tab: `window.open(url, '_blank')`

---

## 11. FOOTER — STANDARD STRUCTURE

Every project footer must include:
- Brand name or logo
- Brief tagline or description (1 line)
- Quick navigation links
- Contact information (WhatsApp, email, address if applicable)
- Social media icons with real links
- Legal links (Términos y Condiciones, Política de Privacidad)
- **"Powered by Vyper Studio"** — small, subtle text, no link
- Copyright: `© [YEAR] [Brand Name]. Todos los derechos reservados.`

Footer background should contrast with the page 
(dark footer on light pages, slightly different dark on dark pages).

---

## 12. SEO — ALWAYS INCLUDE

Every page (including sub-pages in multi-page projects) must have:

```html
<title>[Page Name] | [Brand Name]</title>
<meta name="description" content="[Unique description, 150-160 chars]">
<meta property="og:title" content="[Page Name] | [Brand Name]">
<meta property="og:description" content="[Description]">
<meta property="og:type" content="website">
<meta property="og:image" content="[placeholder or real image URL]">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link rel="canonical" href="[page URL]">
```

Also include:
- Favicon: use a simple placehold.co if no real favicon provided
- Sitemap reference in index.html if multi-page

---

## 13. ACCESSIBILITY (BASIC)

- All images must have descriptive `alt` text
- Buttons must have clear labels (not just icons — add aria-label)
- Color contrast must be readable (avoid light gray text on white)
- Focus states must be visible (don't remove outline completely)
- Interactive elements minimum touch target: 44x44px

---

## 14. PERFORMANCE RULES

- Lazy load all images: `loading="lazy"` on `<img>` tags
- No unnecessary npm packages — prefer CSS and native JS
- Animations use CSS transforms and opacity only 
  (never animate width, height, or margin)
- No `!important` in custom CSS — use Tailwind specificity
- Keep component files focused: one component = one responsibility

---

## 15. BRANDING — VYPER STUDIO

**Always in the footer, small and subtle:**
```
Powered by Vyper Studio
```
No link, no bold, no color highlight — just small gray text.

**Copyright format:**
```
© 2026 [Client Brand]. Todos los derechos reservados.
```

---

## QUICK REFERENCE — WHAT NOT TO DO

| ❌ Never do this | ✅ Do this instead |
|---|---|
| Use TanStack Start | Use Vite + React SPA |
| Use bun | Use npm |
| Use localStorage | Use React state |
| Generate AI images | Use placehold.co |
| Full-screen hero on desktop | min-h-[70vh] max |
| Transparent hamburger menu bg | 100% opaque background |
| Animate width/height | Animate transform/opacity |
| Hardcode admin credentials | Use Supabase Auth |
| Leave image sections empty | Always add placeholders |
| Crowd mobile navbar with icons | Put extras inside drawer |
| Single font size for all text | Clear h1 > h2 > h3 hierarchy |
