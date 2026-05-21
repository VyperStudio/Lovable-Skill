---
name: Vyper-Studio-Standards
description: Use when creating any web project, page, section, or component for Vyper Studio clients. Applies design standards, technical stack, animation rules, and branding requirements automatically.
---

# Vyper Studio — Development Standards

## 1. TECHNICAL STACK (NON-NEGOTIABLE)

- **Framework:** Vite + React SPA — NEVER TanStack Start, NEVER Next.js
- **Routing:** React Router DOM (multi-page projects only)
- **Styles:** Tailwind CSS
- **Package manager:** npm — NEVER bun, delete bun.lockb if present
- **Always include vercel.json at project root:**
  `{ "rewrites": [{ "source": "/(.*)", "destination": "/index.html" }] }`
- **State management:** React state (useState, useContext) — NEVER localStorage, NEVER sessionStorage
- **Icons:** lucide-react preferred
- **Deployment:** Compatible with Vercel and Cloudflare Pages

---

## 2. IMAGES — CRITICAL RULES

NEVER generate, create, or hallucinate images. Always use placehold.co:

- Hero background: `placehold.co/1920x1080/0A0A0A/333333`
- Product card portrait: `placehold.co/400x500/1A1A1A/444444`
- Team member square: `placehold.co/400x400/1A1A1A/444444`
- Gallery image: `placehold.co/600x600/1A1A1A/333333`
- Event banner: `placehold.co/800x400/1A1A1A/444444`

Color the placeholder background close to the project palette so the layout feels intentional. Never use Unsplash, Pexels, AI-generated images, or random URLs.

---

## 3. HERO SECTIONS — SIZE AND PROPORTIONS

Desktop heroes must NOT be full-screen unless explicitly requested.

- Main hero (home): `min-h-[70vh]` — never `100vh` on desktop
- Sub-page hero: `py-24 md:py-32` — compact, not full screen
- Mobile: `min-h-[80vh]` is acceptable
- Never leave dead space above or below hero content — reduce padding if needed

---

## 4. HAMBURGER MENU — FLEXIBLE BUT ALWAYS FUNCTIONAL

Style can vary per project, but must ALWAYS meet these rules:

- Opens with smooth animation: `transition: transform 0.3s ease-in-out`
- Background is 100% opaque — NEVER transparent
- Dark overlay behind: `rgba(0,0,0,0.6)` minimum
- Clicking overlay closes the menu
- `body` gets `overflow: hidden` while menu is open
- Smooth scroll to section when nav link is tapped
- Links cascade with 0.05s delay between each

Style options:
- Slide from right (default): `translateX(100%) → translateX(0)`, width 80vw
- Full screen overlay (premium): `opacity: 0 → 1`, width 100vw
- Slide from left: `translateX(-100%) → translateX(0)`, width 75vw

For professional/personal sites: white background drawer, black text, clean typography (reference: Dr. Alejandro Vargas demo style).

---

## 5. ANIMATIONS — GLOBAL RULES

- Scroll reveal: `opacity: 0 → 1` + `translateY(20px) → translateY(0)`, duration 0.5s ease-out
- Stagger between cards: 0.08s delay increment
- Intersection Observer threshold: 0.12, always `once: true`
- Hover on cards: `translateY(-4px)` to `-6px`, duration 0.25s
- Page transitions: fade + `scale(0.98 → 1)` in 0.2s
- Loading states: skeleton screens (not spinners)

Never do:
- No bouncing or elastic animations
- No animations longer than 0.8s for UI elements
- No infinitely repeating animations that distract
- Never animate width, height, or margin — only transform and opacity

---

## 6. LAYOUT AND SPACING

- Section padding mobile: `py-16 px-4`
- Section padding desktop: `py-24 px-8` or `py-32 px-16`
- Max content width: `max-w-6xl mx-auto`
- Text-heavy sections: `max-w-3xl mx-auto`
- Cards grid: `grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6`
- Two-column: `grid-cols-1 md:grid-cols-2 gap-12`
- Never let text span full viewport width on desktop
- Never leave empty-feeling sections — add a divider or reduce padding

---

## 7. TYPOGRAPHY

- Maximum 2 font families per project
- Load via Google Fonts link in index.html
- Clear hierarchy: h1 much larger than h2, h2 clearly larger than h3
- Body text minimum: 16px, line-height: 1.6 to 1.8
- Never use font-size below 12px
- Uppercase labels: letter-spacing 0.1em to 0.2em
- Maximum 3 font weights per project

---

## 8. NAVIGATION

Desktop:
- Fixed position, background changes on scroll (transparent to solid + shadow)
- Active link indicator (underline or color)
- CTA button on the right

Mobile:
- Logo left, hamburger right
- Social icons go inside drawer, not in the top bar
- CTA button at bottom of drawer, prominently styled

---

## 9. SUPABASE INTEGRATION

Connection order: Connect Supabase in Lovable settings BEFORE sending any prompt.

Auth rules:
- Always use `supabase.auth.signInWithPassword()`
- Always use `supabase.auth.signOut()`
- Check `supabase.auth.getSession()` on mount, redirect if not authenticated
- Never hardcode credentials in frontend code

Storage rules:
- Images: always `object-contain` not `object-cover`
- Portrait images: `aspect-[4/5]`
- Landscape: `aspect-[16/9]`
- Square: `aspect-square`

Admin panel:
- NO visible link in navbar or footer
- Login at `/admin`
- Always include logout button inside panel

---

## 10. FORMS

- Required fields with visible validation
- Inline error messages below each field (not alerts)
- Button states: "Enviar" → "Enviando..." → "Enviado!"
- Disable button while submitting
- Input minimum height: 44px
- Focus state: border changes to accent color

WhatsApp forms:
- Build message string from fields
- Use `encodeURIComponent()` on message
- Open: `https://wa.me/[NUMBER]?text=[ENCODED_MESSAGE]`
- Always open in new tab

---

## 11. FOOTER — ALWAYS INCLUDE

- Brand name or logo
- Brief tagline (1 line)
- Quick navigation links
- Contact info (WhatsApp, email, address if applicable)
- Social media icons with real links
- Legal links (Términos y Condiciones, Política de Privacidad)
- `Powered by Vyper Studio` — small, subtle, no link, no bold
- Copyright: `© 2026 [Brand]. Todos los derechos reservados.`

---

## 12. SEO — EVERY PAGE

Include on every page:
- `<title>[Page] | [Brand]</title>`
- `<meta name="description" content="[150-160 chars]">`
- Open Graph: og:title, og:description, og:type, og:image
- `<meta name="viewport" content="width=device-width, initial-scale=1.0">`
- Favicon: use placehold.co if no real favicon provided

---

## 13. ACCESSIBILITY

- All images: descriptive `alt` text
- Icon-only buttons: add `aria-label`
- Readable color contrast — no light gray on white
- Visible focus states — never remove outline completely
- Minimum touch target: 44x44px

---

## 14. PERFORMANCE

- All images: `loading="lazy"`
- No unnecessary npm packages
- Animations use only transform and opacity
- No `!important` in custom CSS

---

## 15. QUICK REFERENCE

| Never do this | Do this instead |
|---|---|
| TanStack Start or Next.js | Vite + React SPA |
| bun as package manager | npm |
| localStorage or sessionStorage | React state |
| Generate or hallucinate images | placehold.co |
| Full-screen hero on desktop | min-h-70vh maximum |
| Transparent hamburger background | 100% opaque |
| Animate width or height | Animate transform and opacity only |
| Hardcode admin credentials | Supabase Auth |
| Leave image sections empty | Always add placeholders |
| Social icons crowding mobile navbar | Put extras inside drawer |
