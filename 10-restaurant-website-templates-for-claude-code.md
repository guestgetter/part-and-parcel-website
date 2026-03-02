# 10 Restaurant Website Templates to Build with Claude Code

**GSAP-Animated, SEO-Optimized, Immersive Single-Page Sites**

Each template below is designed to be built as a single HTML file with inline CSS and JS — perfect for Claude Code development. They use GSAP + ScrollTrigger from CDN, semantic HTML for SEO, and Restaurant schema markup baked in.

---

## The SEO Foundation (Include in Every Template)

Every template should include this baseline:

**Semantic HTML:** `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>` — never `<div>` soup.

**Restaurant Schema Markup (JSON-LD):**
```json
{
  "@context": "https://schema.org",
  "@type": "Restaurant",
  "name": "Restaurant Name",
  "image": "hero-image.jpg",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "123 Main St",
    "addressLocality": "City",
    "addressRegion": "ST",
    "postalCode": "12345"
  },
  "telephone": "(555) 123-4567",
  "url": "https://restaurant.com",
  "servesCuisine": ["Italian", "Mediterranean"],
  "priceRange": "$$",
  "openingHours": ["Mo-Sa 11:00-22:00", "Su 10:00-21:00"],
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": "4.7",
    "reviewCount": "312"
  },
  "hasMenu": "https://restaurant.com/#menu",
  "acceptsReservations": "True"
}
```

**Meta Tags:**
```html
<title>Restaurant Name | Best [Cuisine] in [City] | Reservations</title>
<meta name="description" content="Award-winning [cuisine] in [neighborhood]. Fresh, locally-sourced ingredients. Open [hours]. Reserve your table today.">
<meta name="viewport" content="width=device-width, initial-scale=1">
<link rel="canonical" href="https://restaurant.com">
```

**GSAP CDN Setup:**
```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/ScrollTrigger.min.js"></script>
```

---

## Template 1: "The Origin Story" — Scroll-Driven Narrative

**Concept:** A vertical storytelling journey from farm/source → kitchen → plate → table. The user scrolls through the restaurant's origin story like chapters of a book. Each scroll section reveals a new chapter with parallax images and text animations.

**Vibe:** Dishoom meets Noma. Warm, nostalgic, deeply human.

**Sections:**
1. **Hero** — Full-bleed image with restaurant name. Text fades in on load with staggered letter animation.
2. **Chapter 1: "Where It Began"** — Origin story with parallax background image. Text slides in from the left as you scroll.
3. **Chapter 2: "The Kitchen"** — Chef profile with image reveal (clip-path animation expanding from center).
4. **Chapter 3: "The Menu"** — Menu items appear one by one as you scroll, each with a subtle scale-up.
5. **Chapter 4: "The Table"** — Reservation CTA with location map and hours.
6. **Footer** — Contact, social links, schema markup.

**Key GSAP Animations:**
```javascript
// Staggered text reveal per chapter
gsap.from(".chapter-text", {
  y: 80, opacity: 0, duration: 1.2, stagger: 0.15,
  scrollTrigger: { trigger: ".chapter", start: "top 80%", end: "top 30%", scrub: 1 }
});

// Parallax background images
gsap.to(".parallax-bg", {
  yPercent: -30, ease: "none",
  scrollTrigger: { trigger: ".chapter", scrub: true }
});

// Image reveal with clip-path
gsap.from(".chef-image", {
  clipPath: "circle(0% at 50% 50%)", duration: 1.5,
  scrollTrigger: { trigger: ".chef-section", start: "top 60%" }
});
```

**SEO Power:** Long-form storytelling content naturally ranks for "[restaurant name] story," "best [cuisine] in [city]," and chef-related queries. Semantic headings create clear content hierarchy.

**Best For:** Farm-to-table, heritage restaurants, chef-driven concepts.

---

## Template 2: "The Dark Room" — Moody Fine Dining Reveal

**Concept:** Black background. Content emerges from darkness as you scroll — like walking into a dimly lit restaurant. Images illuminate as they enter the viewport. Text glows subtly.

**Vibe:** Eleven Madison Park meets Gaggan. Cinematic. Mysterious.

**Sections:**
1. **Hero** — Black screen. Restaurant name fades in letter-by-letter in gold/cream. Subtle grain texture overlay.
2. **Philosophy** — A single sentence revealed word-by-word as you scroll (scrubbed animation).
3. **Signature Dishes** — Horizontal scroll gallery pinned in place. Each dish image fades from black with a soft glow effect.
4. **Tasting Menu** — Menu items appear in an elegant stacked layout, each sliding up from opacity 0.
5. **Ambiance** — Full-bleed interior photo with parallax. Reservation button pulses gently.
6. **Footer** — Minimal. Just address, phone, hours.

**Key GSAP Animations:**
```javascript
// Word-by-word philosophy reveal
const words = document.querySelectorAll(".philosophy-word");
gsap.from(words, {
  opacity: 0, y: 20, stagger: 0.08,
  scrollTrigger: { trigger: ".philosophy", start: "top 70%", end: "bottom 40%", scrub: true }
});

// Horizontal scroll gallery (pinned)
let sections = gsap.utils.toArray(".dish-panel");
gsap.to(sections, {
  xPercent: -100 * (sections.length - 1), ease: "none",
  scrollTrigger: { trigger: ".gallery-wrapper", pin: true, scrub: 1,
    end: () => "+=" + document.querySelector(".gallery-wrapper").offsetWidth }
});

// Dish image glow reveal
gsap.from(".dish-image", {
  opacity: 0, scale: 0.95, filter: "brightness(0)",
  duration: 1.5, stagger: 0.3,
  scrollTrigger: { trigger: ".dish-grid", start: "top 75%" }
});
```

**SEO Power:** Rich alt text on dish images. Menu items as crawlable text (not images). Schema markup for menu with `hasMenu` property.

**Best For:** Fine dining, tasting menus, Michelin-level concepts, speakeasies.

---

## Template 3: "The Neighborhood Joint" — Warm & Inviting Single-Pager

**Concept:** Feels like a friend's recommendation. Warm colors (cream, terracotta, sage). Friendly typography. Sections scroll naturally with gentle fade-ins. No over-the-top effects — just smooth, confident simplicity.

**Vibe:** Founding Farmers meets Sunday in Brooklyn. Comfort food energy.

**Sections:**
1. **Hero** — Warm photo of restaurant interior/exterior. Name + tagline with a slight bounce-in.
2. **Welcome** — Short paragraph with owner's photo. Fades in on scroll.
3. **Menu Highlights** — 3-4 featured dishes in a responsive grid. Cards scale up gently on scroll.
4. **Daily Specials** — Rotating banner with today's special. Subtle slide animation.
5. **Reviews** — 3 customer testimonials that slide in from alternating sides.
6. **Visit Us** — Map embed, hours, phone. Big "Order Online" and "Reserve" buttons.
7. **Footer** — Newsletter signup, social links, address.

**Key GSAP Animations:**
```javascript
// Gentle staggered card reveals
gsap.from(".menu-card", {
  y: 40, opacity: 0, scale: 0.95, duration: 0.8, stagger: 0.2,
  scrollTrigger: { trigger: ".menu-grid", start: "top 80%" }
});

// Alternating testimonial slides
gsap.utils.toArray(".testimonial").forEach((t, i) => {
  gsap.from(t, {
    x: i % 2 === 0 ? -60 : 60, opacity: 0, duration: 1,
    scrollTrigger: { trigger: t, start: "top 85%" }
  });
});

// CTA button pulse
gsap.to(".cta-button", {
  scale: 1.05, duration: 0.8, repeat: -1, yoyo: true, ease: "sine.inOut"
});
```

**SEO Power:** Testimonials with Review schema. LocalBusiness schema with full address. FAQ section potential for "People Also Ask" rich results.

**Best For:** Casual dining, family restaurants, neighborhood bistros, cafes.

---

## Template 4: "The Ingredient Journey" — Scroll-Pinned Ingredient Showcase

**Concept:** Each section pins in place and reveals an ingredient's story — where it's sourced, how it's prepared, what dish it becomes. Scroll to progress through each ingredient's transformation. Think Apple product pages but for food.

**Vibe:** Pujol meets Salt & Straw. Craft-focused. Ingredient worship.

**Sections:**
1. **Hero** — Close-up macro shot of a key ingredient (e.g., tomato, olive, spice). Name and tagline overlay.
2. **Ingredient 1** (Pinned Section) — Three stages revealed on scroll: Source → Preparation → Dish. Each stage has its own image and text block that fades/slides into view.
3. **Ingredient 2** (Pinned Section) — Same structure, different ingredient.
4. **Ingredient 3** (Pinned Section) — Same structure, different ingredient.
5. **Full Menu** — Clean text menu with pricing. Anchored section.
6. **The Team** — Chef and team photos with name/role reveals.
7. **Reserve** — Embedded reservation widget or link.

**Key GSAP Animations:**
```javascript
// Pinned ingredient transformation
gsap.utils.toArray(".ingredient-section").forEach(section => {
  let stages = section.querySelectorAll(".stage");
  let tl = gsap.timeline({
    scrollTrigger: {
      trigger: section, pin: true, scrub: 1,
      end: () => "+=" + (stages.length * window.innerHeight)
    }
  });
  stages.forEach((stage, i) => {
    if (i > 0) {
      tl.from(stage, { opacity: 0, y: 100, duration: 1 })
        .to(stages[i-1], { opacity: 0, y: -50, duration: 0.5 }, "<");
    }
  });
});
```

**SEO Power:** Long-form content about sourcing and preparation naturally targets "[ingredient] + [city]" and "farm-to-table [city]" queries. Image alt text describes ingredient sourcing.

**Best For:** Farm-to-table, organic/sustainable restaurants, craft cocktail bars, artisan bakeries.

---

## Template 5: "The Culture Capsule" — Immersive Cultural Experience

**Concept:** Transport the visitor to another place. Full-bleed cultural imagery, pattern borders inspired by the cuisine's origin (e.g., Japanese wave patterns, Mexican tile patterns, Indian mandala borders). Text reveals timed to feel like you're walking through the culture.

**Vibe:** Dishoom meets Tacombi. Cultural storytelling as the product.

**Sections:**
1. **Hero** — Cultural pattern animation fills the screen, then parts to reveal the restaurant name and a hero image. Like curtains opening.
2. **Our Heritage** — Cultural backstory with scroll-triggered image reveals. Photos of the home country/region.
3. **The Experience** — What to expect when you visit. Interior photos with parallax.
4. **Signature Menu** — Dishes presented with cultural context (short origin story for each dish).
5. **The Ritual** — How to eat here. A guide to the dining experience (e.g., "how to order at an izakaya"). Interactive scroll.
6. **Events & Catering** — Upcoming events, private dining options.
7. **Footer** — Multi-language support indication, social, location.

**Key GSAP Animations:**
```javascript
// Cultural curtain reveal on hero
gsap.to(".curtain-left", { xPercent: -100, duration: 1.5, ease: "power4.inOut" });
gsap.to(".curtain-right", { xPercent: 100, duration: 1.5, ease: "power4.inOut" });
gsap.from(".hero-content", { opacity: 0, scale: 0.9, duration: 1, delay: 1 });

// Decorative border pattern animation
gsap.to(".pattern-border", {
  backgroundPosition: "200% 0", duration: 20, repeat: -1, ease: "none"
});

// Dish cards with cultural context
gsap.from(".dish-story", {
  x: -80, opacity: 0, duration: 1, stagger: 0.3,
  scrollTrigger: { trigger: ".menu-section", start: "top 70%" }
});
```

**SEO Power:** Cultural keywords naturally rank for "authentic [cuisine] [city]," "[culture] dining experience," and "[dish name] origin." Rich content about dining rituals targets informational queries.

**Best For:** Ethnic restaurants, cultural dining concepts, izakayas, trattorias, taquerias, dim sum houses.

---

## Template 6: "The Time Machine" — Seasonal/Time-Based Design

**Concept:** The website changes based on the time of day or season. Morning shows brunch vibes (light, airy). Evening shows dinner atmosphere (dark, candlelit). Scroll reveals the restaurant through different times of day. Background color transitions from dawn to dusk as you scroll.

**Vibe:** Attica meets Noma. Time-aware. Living, breathing design.

**Sections:**
1. **Hero** — Background gradient shifts from morning gold to evening deep blue as time passes (or as user scrolls). Restaurant name centered.
2. **Right Now** — Dynamic section showing current menu (brunch/lunch/dinner based on time). Auto-updates.
3. **Morning at [Name]** — Brunch menu + light photography. Warm yellows.
4. **Afternoon at [Name]** — Lunch menu. Transition zone.
5. **Evening at [Name]** — Dinner menu. Deep tones. Candlelit photography.
6. **This Season** — Seasonal specials highlighted. Ingredient availability.
7. **Reserve Your Moment** — Time-picker reservation CTA.

**Key GSAP Animations:**
```javascript
// Dawn-to-dusk background transition on scroll
gsap.to("body", {
  background: "linear-gradient(180deg, #1a1a2e 0%, #16213e 50%, #0f3460 100%)",
  scrollTrigger: { trigger: "main", start: "top top", end: "bottom bottom", scrub: true }
});

// Menu section crossfades based on scroll position
gsap.utils.toArray(".time-section").forEach((section, i) => {
  gsap.from(section, {
    opacity: 0, duration: 1,
    scrollTrigger: { trigger: section, start: "top 60%", end: "top 20%", scrub: true }
  });
});

// Candle flicker effect (CSS animation triggered by GSAP)
gsap.to(".candle-glow", {
  opacity: 0.7, duration: 0.3, repeat: -1, yoyo: true,
  ease: "rough({ strength: 1, points: 20, template: none, taper: none, randomize: true })"
});
```

**SEO Power:** Separate sections for brunch, lunch, and dinner menus target time-specific queries ("brunch near me," "dinner reservations [city]"). Seasonal content stays fresh for crawlers.

**Best For:** All-day restaurants, brunch spots, restaurants with rotating seasonal menus.

---

## Template 7: "The Retro Arcade" — Playful & Interactive

**Concept:** Inspired by Royal Sushi's 8-bit approach. Playful, gamified experience with pixel art accents, retro color palettes, and interactive hover effects. Not childish — retro-cool. Menu items have fun hover animations. Easter eggs hidden throughout.

**Vibe:** Royal Sushi & Izakaya meets Dirty Bones. Nightlife energy with a wink.

**Sections:**
1. **Hero** — Pixelated logo animation that "renders" into the real logo. Retro color burst.
2. **The Vibe** — Tagline with typewriter text effect. Neon glow accents.
3. **Menu** — Menu items styled as "game levels" or "power-ups." Hover effects reveal dish photos.
4. **Specials** — Slot machine-style rotating daily specials.
5. **Gallery** — Polaroid-style image grid. Images tilt on hover and stack with depth.
6. **Find Us** — Pixel-art map illustration with real address overlay.
7. **Footer** — "Insert Coin" reservation button. Social links as game icons.

**Key GSAP Animations:**
```javascript
// Pixel-to-real logo morph
gsap.from(".logo", {
  filter: "blur(8px) contrast(200%)", scale: 1.2,
  duration: 2, ease: "steps(8)"
});

// Typewriter effect
const text = "Welcome to the game.";
gsap.to(".typewriter", {
  duration: text.length * 0.08,
  text: { value: text, delimiter: "" },
  ease: "none"
});

// Menu items cascade in like Tetris blocks
gsap.from(".menu-item", {
  y: -200, opacity: 0, rotation: () => gsap.utils.random(-15, 15),
  stagger: { amount: 1, from: "random" },
  scrollTrigger: { trigger: ".menu-section", start: "top 70%" }
});
```

**SEO Power:** Unique, share-worthy design generates backlinks. Strong brand queries. Interactive elements increase time-on-page (positive ranking signal).

**Best For:** Ramen bars, burger joints, tiki bars, dive bars, pop-up concepts, food trucks with attitude.

---

## Template 8: "The Minimal Gallery" — Photography-First Design

**Concept:** Let the food speak. Massive full-bleed photography with minimal text. White space as a design element. Each scroll section is essentially one gorgeous photo with a single line of copy. The website is a curated gallery of the restaurant's best moments.

**Vibe:** The Clove Club meets Adachi. Quiet confidence. The food IS the design.

**Sections:**
1. **Hero** — Single stunning dish photo, full viewport. Restaurant name in elegant thin serif.
2. **Photo 1** — Kitchen action shot. One-line caption fades in.
3. **Photo 2** — Interior detail. Caption.
4. **Photo 3** — Signature dish plating.
5. **The Menu** — Clean, text-only menu in a centered column. No photos in this section — intentional contrast.
6. **Photo 4** — Exterior/location shot with address overlay.
7. **Reserve** — Minimal form. Just date, time, party size.

**Key GSAP Animations:**
```javascript
// Full-viewport image parallax
gsap.utils.toArray(".gallery-section").forEach(section => {
  const img = section.querySelector("img");
  gsap.fromTo(img,
    { yPercent: -15 },
    { yPercent: 15, ease: "none",
      scrollTrigger: { trigger: section, scrub: true } }
  );
});

// Caption fade-in
gsap.from(".caption", {
  opacity: 0, y: 30, duration: 1.5, ease: "power2.out",
  scrollTrigger: { trigger: ".caption", start: "top 85%" }
});

// Snap to each photo section
ScrollTrigger.create({
  snap: 1 / (document.querySelectorAll(".gallery-section").length - 1),
  duration: 0.5, ease: "power1.inOut"
});
```

**SEO Power:** Heavy image optimization with descriptive alt text targets Google Image Search. Minimal text means what IS there carries maximum keyword weight. Clean URLs and fast load times.

**Best For:** Fine dining, pastry shops, wine bars, any restaurant with exceptional photography.

---

## Template 9: "The Neighborhood Map" — Location-Anchored Storytelling

**Concept:** The restaurant in context of its neighborhood. Scroll reveals the restaurant's relationship to the community — nearby landmarks, local suppliers, the walk from the subway. Builds a sense of place that makes you want to visit the AREA, not just the restaurant.

**Vibe:** Mei Mei meets Sunday in Brooklyn. Community-rooted. "Come for the neighborhood, stay for the food."

**Sections:**
1. **Hero** — Illustrated or stylized map of the neighborhood with the restaurant marked. Zoom-in animation on load.
2. **The Block** — "Here's what's around us" — nearby points of interest with walking distances. Scroll reveals each one.
3. **Our Story Here** — How the restaurant fits into the neighborhood's history.
4. **Local Partners** — Suppliers, farmers, producers with their stories. Supporting cast reveals.
5. **The Menu** — Standard menu section with local sourcing callouts.
6. **Getting Here** — Transit directions, parking info, with animated route lines.
7. **Footer** — Embedded map, hours, contact.

**Key GSAP Animations:**
```javascript
// Map zoom-in on load
gsap.from(".neighborhood-map", {
  scale: 3, opacity: 0, duration: 2.5, ease: "power3.out"
});

// Animated route lines (SVG path drawing)
gsap.from(".route-path", {
  strokeDashoffset: (i, el) => el.getTotalLength(),
  duration: 2,
  scrollTrigger: { trigger: ".directions-section", start: "top 60%" }
});

// Partner cards fan out from center
gsap.from(".partner-card", {
  scale: 0, rotation: () => gsap.utils.random(-30, 30),
  stagger: 0.15, duration: 0.8,
  scrollTrigger: { trigger: ".partners-grid", start: "top 75%" }
});
```

**SEO Power:** This is an SEO monster. Neighborhood keywords, "near me" queries, local landmark associations, supplier partnerships (potential backlinks), transit/parking info that answers common local queries. LocalBusiness schema with GeoCoordinates.

**Best For:** Neighborhood restaurants, restaurants in destination neighborhoods, restaurants near landmarks or attractions.

---

## Template 10: "The Chef's Table" — Interactive Tasting Experience

**Concept:** The website IS a tasting menu experience. Each scroll section is a "course" with paired content — a dish image, tasting notes, wine pairing, and chef's commentary. Progress bar at the side shows which course you're on. Feels like sitting at the chef's counter.

**Vibe:** Ultraviolet by Paul Pairet meets Attica. Multi-sensory. Experiential.

**Sections:**
1. **Amuse-Bouche** (Hero) — Welcome message from the chef. Elegant entrance animation.
2. **Course 1** — First dish with tasting notes panel. Image zooms in from slightly out of focus to sharp.
3. **Course 2** — Second dish. Wine pairing suggestion slides in from the side.
4. **Course 3** — Third dish. Chef's audio note (play button with waveform animation).
5. **Course 4** — Dessert. Color palette shifts to warmer tones.
6. **Digestif** — Thank you + reservation CTA. "Book your seat at the table."
7. **Progress Indicator** — Fixed sidebar showing course position (like a tasting menu card).

**Key GSAP Animations:**
```javascript
// Course transition with focus shift
gsap.from(".course-image", {
  filter: "blur(8px)", scale: 1.1, duration: 1.5,
  scrollTrigger: { trigger: ".course", start: "top 60%", end: "top 20%", scrub: true }
});

// Tasting notes typewriter reveal
gsap.from(".tasting-note span", {
  opacity: 0, y: 10, stagger: 0.05,
  scrollTrigger: { trigger: ".tasting-note", start: "top 75%" }
});

// Progress indicator
gsap.to(".progress-fill", {
  scaleY: 1, transformOrigin: "top",
  scrollTrigger: { trigger: "main", start: "top top", end: "bottom bottom", scrub: true }
});

// Color palette shift for dessert
gsap.to(".course-dessert", {
  backgroundColor: "#2d1b14",
  scrollTrigger: { trigger: ".course-dessert", start: "top 80%", end: "top 20%", scrub: true }
});
```

**SEO Power:** Detailed tasting notes and wine pairings target long-tail queries like "[restaurant] tasting menu," "best wine pairing [dish]," "[cuisine] tasting experience [city]." Chef content builds E-E-A-T (Experience, Expertise, Authority, Trust).

**Best For:** Tasting menu restaurants, omakase, chef's table concepts, wine-pairing-forward dining.

---

## Build Priorities for Guest Getter Clients

When choosing which template to develop first, consider the client's positioning:

| Client Type | Best Template | Why |
|---|---|---|
| **Amano Trattoria** | #5 Culture Capsule or #1 Origin Story | Italian heritage storytelling is a natural fit |
| **In Good Spirits** | #2 Dark Room or #7 Retro Arcade | Bar/cocktail vibe needs mood or personality |
| **Joyo Burger** | #3 Neighborhood Joint or #7 Retro Arcade | Casual brand needs warmth or playfulness |
| **Fine Dining Client** | #2 Dark Room or #10 Chef's Table | Premium positioning demands restraint and craft |
| **Farm-to-Table Client** | #4 Ingredient Journey or #1 Origin Story | Sourcing story IS the differentiator |

## Technical Implementation Notes

**Performance:** Keep total page weight under 3MB. Lazy-load images below the fold. Use WebP format. GSAP itself is only ~30KB gzipped.

**Mobile:** All GSAP animations should be simplified or disabled on mobile. Use `ScrollTrigger.matchMedia` to set responsive breakpoints:
```javascript
ScrollTrigger.matchMedia({
  "(min-width: 768px)": function() { /* desktop animations */ },
  "(max-width: 767px)": function() { /* simpler mobile animations */ }
});
```

**Accessibility:** Respect `prefers-reduced-motion`. Always:
```javascript
const prefersReducedMotion = window.matchMedia("(prefers-reduced-motion: reduce)").matches;
if (prefersReducedMotion) { gsap.globalTimeline.timeScale(0); }
```

**Deployment:** Each template is a single HTML file. Host on any static host (Netlify, Vercel, even shared hosting). No build step required. Swap in client photos and content to customize.

---

*Built for Guest Getter's restaurant clients. Each template is designed to be developed in a single Claude Code session and deployed same-day.*
