[中文](USAGE.md) | [English](USAGE.en.md)

# Usage Checklist — Get Good Results With Zero Design Experience

This isn't the rules file the Skill reads (`skills/finesse-ui/SKILL.md` — thousands of lines of internal decision logic you don't need to read). This one is for **you**: how to phrase the ask, what it replies with, how to confirm direction, how to iterate, how to keep a multi-page project consistent, and how to do a final check. Read it once, then use it as a reference.

---

## Apple design language (0.22.0)

Choose Apple as a design language over brand, product, commerce or h5. Select editorial for product stories, app for functional interfaces, or spatial for explicitly requested depth/materials. “Apple style” does not automatically add glass, Bento or 3D.

- [Design rules](skills/finesse-ui/references/apple-design.md): typography, neutral surfaces, corners, materials and scoped default overrides.
- [Layout recipes](skills/finesse-ui/references/apple-patterns.md): cards, Bento, contrast, spacing and galleries.
- [Seven interactive studies](skills/finesse-ui/examples/apple-overview.html): bundled styles, scripts and media for offline viewing. Keep the adjacent `apple/` and `lib/` folders.
- Gestures reuse the shared interaction reference with interruption, velocity handoff and projected detents. The detector only exempts the pure-black/white hint for explicitly stamped Apple files; other checks still run.

Product imagery and figures are educational composition material. Third-party imagery is not relicensed by the repository MIT license; see [asset notes](skills/finesse-ui/examples/apple/ASSETS.md) and use appropriate project assets in production.

### Prompts to try

> Build an Apple-inspired product page with white/gray surfaces, one dominant product image and a mobile reflow.
> Make this settings page Apple-inspired while preserving its form structure.
> Create a spatial tool panel; use translucency only for chrome and keep reading surfaces clear.

For an existing component, say “change only this component.” Ask for reduced-motion, keyboard, mobile reading-order and dialog focus-return checks at delivery.

## The 30-second version

1. State the **page type** (landing/dashboard/portfolio/commerce) + **1-2 mood words**.
2. It tells you **what you'll see** and names the two things most likely to be wrong — **it only starts writing code once you confirm.** Can't say what you want? Say so, and it builds three directions for you to look at.
3. Don't say "redo it" — **point at the specific thing you don't like** (one sentence, e.g. "too plain"); it fixes only that.
4. Building a whole page set? Say "keep these consistent" up front — it locks a spec, and tells you what got locked and how to unlock it.
5. Before shipping it checks the built page against that "what you'll see" line; you can also say `audit` any time for a read-only diagnostic — it reports, you decide what to fix.

Each point is expanded below.

---

## 1. Your first message: how to describe what you need

### 1.1 State the page type first — this is the single most important sentence

finesse splits pages into genuinely different routes. Naming the type tells it which logic to apply:

| Type | What it is | Examples | Layout thinking |
|---|---|---|---|
| **brand (landing/marketing)** | Design IS the product — landing pages, brand sites, launches, portfolios, industry hero pages | "A landing page for a yoga studio", "a photographer's personal portfolio", "a product launch page" | Goes for spectacle and first impression, one point per screen, reaches for a real visual engine (3D particles / Canvas motion / GSAP scroll storytelling) |
| **product (dashboard/app)** | Design SERVES the product — dashboards, admin panels, data analytics, settings pages | "A data dashboard for our ops team", "an order-management page for an e-commerce backend", "a SaaS admin panel" | Goes for clarity and information density, no showing off — charts/tables/forms need to survive daily use |
| **commerce (selling pages)** | Pages that sell something — product detail pages, listing pages, cart, checkout | "A flagship product's detail page", "a filterable product listing page", "the checkout flow" | Selling one item leans brand (needs a vibe); listing/filter pages lean product (density, efficiency first) |
| **h5 (phone-only pages)** | Pages that only ever open on a phone — campaign H5s, mini-program / in-app screens, app UI prototypes, mobile PDPs, report H5s | "A Black Friday campaign page", "design the UI for a budgeting app", "a product detail page for mobile", "a year-in-review H5" | Builds on a real phone (390×844) first, then applies one of the three routes above for content. Primary buttons always go to the **bottom** (thumb reach), and it's built to actually feel like an app: status bar, bottom TabBar, sheets that slide up, detail pages that push in from the right |

**The one thing to be clear about on the h5 route: is this page phone-only?** "It should look good on a phone too" and "it only ever opens on a phone" are different jobs — the first is a normal page with proper mobile handling, only the second goes h5. If you can't tell, that's fine: finesse will ask you *"does this page only open on a phone, or does it need to look good on a desktop too?"*

**Not sure which bucket?** Just say so — "I'm not sure if this should feel more presentation-oriented or more tool-y" — and it will ask a clarifying question rather than guess blindly.

### 1.2 Mood words: give 1-2 of the most important ones, not a pile

Internally, finesse converts your adjectives into three "dials" — **SOUL** (how distinct the personality is), **SPECTACLE** (how technically ambitious the visuals are), **DENSITY** (information per screen). Precise words convert cleanly; a pile of adjectives fights itself. Roughly, here's how common words get read (no need to memorize — just know this mapping exists):

| You say | Roughly translates to |
|---|---|
| "premium", "luxury", "high-end" | Distinct style, moderate motion, not too dense — a boutique feel |
| "minimal", "clean", "understated" | Quieter style, little motion, generous whitespace |
| "bold", "striking", "impactful" | Both style and motion pushed to the max |
| "editorial", "magazine-like" | Careful typography, motion present but not dominant, moderate-to-high content |
| "tech", "AI-ish", "SaaS-y" | Moderate style, stronger motion, medium information density |
| "corporate", "B2B", "enterprise" | Restrained style, almost no showing off, higher information density |
| "playful", "creative", "fun" | Distinct style, moderate-to-strong motion, moderate content |
| "data-heavy", "dashboard-like", "admin-analytics" | Almost no showing off, information density maxed |

- ✅ Good phrasing: "quiet and premium", "bold and striking", "restrained editorial", "warm vintage"
- ❌ Bad phrasing: "minimal but also techy but also warm but also high-end but not too flashy" (too many words and finesse doesn't know which one to prioritize — you get a page that's a bit of everything and a lot of nothing)

If you have a reference in mind ("something like the vibe of [brand]"), naming it or describing the specific image you remember works far better than stacking adjectives.

---

## 2. It tells you what it's about to build — the Design Read

Before finesse writes any code, it **always** stops and describes what it's going to make:

```
Design Read: deep-space astronomy · cinematic + reverent · register=brand · SPECTACLE=8 · engine=Three.js particle galaxy
You'll see: a near-black page with slow-drifting star dust behind everything, a very large
            headline sitting on top of it, and the galaxy rotating as you scroll.
Not right? Most likely one of these: ① you don't want a moving background
            ② near-black is too heavy and you want this light.
Rotation: deliberately steering clear of the last three builds (machined metal / paper press /
          phosphor terminal) — this one is water and drift.
```

**The only line you need to read is `You'll see`.** The `Design Read` line is a coordinate for its own use (`SPECTACLE=8` and the like) — ignore it. The second line is what the page will actually look like.

**This step stops and waits for you to confirm.** Four ways to respond:

1. **"Go ahead"** — only then does it start writing code.
2. **Reply with a number** — e.g. "②, too heavy, our shop is bright." The easiest way to redirect: those two are the mistakes this kind of page most often makes.
3. **Point at the `You'll see` line** — "no moving dust, static is fine", "the headline doesn't need to be that big." No vocabulary required; that line is written entirely in things you can look at.
4. **Add context it missed** — e.g. "this is mainly for older users," and it re-judges with that folded in.

**Why this step matters**: skipping confirmation and saying "whatever, you decide" means that if the direction turns out wrong, redoing it costs far more than the 10 seconds it takes now. It also matters *after* — before delivery, finesse takes that `You'll see` line back and checks the finished page against it clause by clause, so what you get is what you nodded at. The pickier you are here, the more accurate the result.

> **If you genuinely can't say what you want** — you say "I can't really tell", or the only words you have are "premium" / "clean" / "nice" — finesse switches to **building three low-fidelity pages in different directions** for you to look at. Choosing by eye beats choosing by adjective, every time.

---

## 3. After the first draft: how to give feedback and iterate

### 3.1 The core principle — point at it, don't ask for a rebuild

finesse has a set of targeted iteration commands. What you say gets mapped to one of them, **changing only that piece, never rebuilding from scratch**:

| You can say | Maps to | What happens |
|---|---|---|
| "too plain" / "want more impact" / "boring" | `bolder` | Raises SPECTACLE (+2), upgrades the visual engine if needed (e.g. Canvas → Three.js) |
| "too flashy" / "overwhelming" / "exhausting" | `quieter` | Lowers SPECTACLE (−2), swaps to lighter motion or CSS-only |
| "feels off" / "too generic" / "not our vibe" | `soul` | Re-picks the style direction from scratch |
| "too sparse" / "not enough content" | `densify` | Raises information density, adds content |
| "too cluttered" / "too busy" | `densify` (reverse) | Lowers density, trims content, opens up spacing |
| "add a 3D moment" / "want a premium hover" | `depth` | Adds one 3D interaction moment (tilt/flip/depth-parallax cards) without restructuring |
| "want different motion" / "don't like this animation" | `animate` | Swaps the visual engine type, leaves everything else |
| "this one thing looks bad" (a button, a color, a component, some copy) | — | Fixes only what you named, everything else stays |
| "is this page any good? review it" | `audit` | Diagnoses and lists findings, **changes no code** |
| "this page needs an upgrade" | `redesign` | Diagnoses first, then fixes — not a blind full rebuild |

### 3.2 A small trick for clearer feedback

The more specific the feedback, the more accurate the fix:

- ❌ "doesn't feel quite right" — finesse doesn't know where to start
- ✅ "the hero headline is too small, want more presence" — names the area + the problem
- ✅ "overall fine, but the button color clashes with the page" — names the component
- ✅ "this section is cramped on mobile" — names the scenario

### 3.3 Raise one class of issue at a time

If you want both "more impact" and "denser content," you can say both at once — but if you've been sitting on 5 new thoughts after seeing a version, confirm the current direction is right first, then raise them one at a time. Otherwise things get crossed.

---

## 4. Building a whole page set: how to look like "it's from one company"

### 4.1 When you need to "lock" it

If you just need one one-off page, skip this section — steps 1-3 are enough.

But if you're building **a site + a dashboard + a landing page** as a set, or it's a **long-running project** (site this week, product page next week, more pages added next month), say this up front:

> "These pages need to share a consistent look" / "Set up a project spec first, and have later pages follow it"

### 4.2 What happens after you say that

finesse writes a `PRODUCT.md` (the project's long-term memory — industry, users, style direction, locked dial values, what it must never look like) and/or a `design-model.yaml` (the concrete color/type/radius/spacing spec). **You don't need to write or maintain these yourself** — finesse generates and updates them automatically. All you need to know:

- After the first page is built, its colors, fonts, and component look get recorded.
- Before every later page, finesse reads this memory first and follows it — it won't improvise a new palette or font on its own.
- If a later page genuinely needs a different feel (e.g. the dashboard should be more restrained than the marketing site), just say why — finesse records that as a deliberate exception instead of quietly breaking overall consistency.

### 4.3 What if there's already a codebase

If you're not starting from zero and pages already exist, say "check what design system is already in use here" — finesse reads the existing code and reverse-engineers a `design-model.yaml` from it, so new pages follow the established look instead of starting a different one.

---

## 5. Before you ship: the final check

### 5.1 It checks itself against the line you agreed to

Before saying "done," finesse takes the **`You'll see`** line from step 2 and walks the finished page against it, clause by clause:

```
Promise kept
  ✅ deep brown base
  ❌ slow-rising embers  →  shipped as a static background image  →  must fix
  ✅ large serif headline over it
  ✅ uneven-width product cards
```

This exists to catch one specific thing: **the direction quietly drifting mid-build.** On a long page, a moving element can get swapped for a static image because it wouldn't run smoothly, or a dark theme can lighten section by section. Each of those changes looks fine on its own — a static image actually scores *better* on contrast — and only checking against what you originally agreed to will surface it.

### 5.2 You can ask for a check-up any time

Say "check this page for me" or just `audit` — finesse runs a **read-only diagnostic** (changes no code) and scores it against several hard rule categories:

- **Directional consistency** — has the palette drifted, is there a stray second accent color that showed up somewhere
- **Obvious AI tells** — stray em-dashes, gradient text, a wall of identical icon-cards, invented precise-sounding numbers ("92%", "4.1×") with no real data behind them
- **Accessibility/usability** — is text contrast sufficient, are buttons reachable on mobile, is it keyboard-navigable, does motion respect the system's "reduce motion" setting
- **Performance** — will images/animation slow the page down, is there an unwanted horizontal scrollbar on mobile

Findings come back in three tiers, each one saying **what to look for** and **what it costs you**:

| Tier | Means |
|---|---|
| **P0** | ships broken |
| **P1** | clearly reads as AI-generated |
| **P2** | polish |

See the end of Example 1 for the shape. The diagnostic **does not touch code on its own** — you review it and say "fix X first." What to fix and when is always your call.

---

## 6. Three full examples

### Example 1: a brand landing page

```
You: A landing page for a specialty coffee roastery — warm, a little vintage-craft feeling

finesse: Design Read: specialty coffee · warm vintage craft · register=brand · SPECTACLE=5 · engine=Canvas fire particles
         You'll see: a deep brown base, with a small patch of slowly rising embers on the first
                     screen (like the flame inside a roaster), a large serif headline over it,
                     and a row of uneven-width product cards below.
         Not right? Most likely one of these: ① you don't want moving embers
                     ② deep brown is too heavy and you want a light cream base.
         (stops and waits for your confirmation)

You: ②, our shop is very bright — go light

finesse: (re-issues the Design Read on a cream base; only starts coding once you confirm)

You: yes, go ahead

finesse: (generates the full page)

You: overall good, but the first screen feels too plain, want more impact

finesse: (adjusts only the first screen, leaves everything else)

You: can you review how this page is doing?

finesse: audit read-only report: solid structure, but two details are costing you

         P0 — ships broken
           • Button text unreadable on the hero photo (index.html:112)
             On screen: the white "Book a table" label sits on a bright part of the photo.
             Cost: in daylight on a phone it vanishes — your main action disappears.
             → /finesse redesign index.html

         P1 — clearly reads as AI-generated
           • Gradient headline (index.html:47)
             On screen: the main headline fades purple to blue instead of one solid color.
             Cost: the single most-recognized AI-page signature; visitors assume a template.
             → /finesse quieter index.html

         Fix this one first: /finesse redesign index.html — the invisible button is costing
         you bookings today.

You: fix the button first

finesse: (fixes only that)
```

Note the report: every finding tells you **where to look** and **what happens if you leave it**, so you can triage without knowing any terminology.

### Example 2: a product dashboard

```
You: An infrastructure monitoring dashboard for the ops team, dark theme

finesse: Design Read: infrastructure monitoring · calm and precise · register=product · SPECTACLE=2 · component-system
         You'll see: a dark grey base (not pure black), fixed navigation down the left, a row of
                     key numbers across the top, then line charts and a sortable alerts table.
                     Almost no motion.
         Not right? Most likely one of these: ① you want more metrics in that top row
                     ② you want navigation across the top instead of down the left.
         (stops and waits for your confirmation)

You: yes

finesse: (generates a full dashboard: sidebar + charts + data tables)

You: the chart area feels cramped, it's making me dizzy

finesse: densify (reverse) — trims card count, opens up spacing, surfaces the 2-3 most important metrics

You: these pages (monitoring / alerts / settings) need to stay consistent going forward

finesse: Locked for this project: slate-teal accent, Geist headlines, dark theme, left navigation.
         Every later page will follow these. Say "change the accent" (or the type, or the theme)
         and I'll update this page and the ones already built.
```

Note that last reply — finesse tells you **what got locked** and **how to unlock it**. You won't hit the "page five, I want a different color, and it just won't change and I don't know why" situation.

### Example 3: an e-commerce product page

```
You: A product detail page for a flagship pair of headphones, should feel premium

finesse: Design Read: high-end headphones · precision engineering feel · register=commerce(PDP, brand-leaning) · SPECTACLE=6 · engine=product photography + light parallax
         You'll see: a near-black base, one large product shot on the first screen, and as you
                     scroll the image moves slightly slower than the text so it reads as depth;
                     then specs, reviews, and the purchase area.
         Not right? Most likely one of these: ① you want a light base to set the product off
                     ② you don't want the offset-on-scroll effect.
         (stops and waits for your confirmation)

You: yes, go ahead

finesse: (generates the detail page: hero shot + specs + reviews + purchase area)

You: the buy button isn't prominent enough

finesse: (adjusts only the CTA button's visual weight, leaves everything else)
```

---

## 7. FAQ

**Q: I don't know any design terminology, I can only say "looks good / doesn't look good" — is that okay?**
Yes. Two things keep you unstuck: everything it tells you is phrased as *what you'll see*, not as jargon, so you can point at it directly; and if you can't give it a direction at all (only words like "premium" or "nice"), it won't guess — it builds three low-fidelity pages in different directions for you to pick from. Choosing by eye beats choosing by adjective.

**Q: It keeps using words I don't know (eyebrow, grain, contrast ratio) — do I need to learn them?**
No. The first time any of them appears, it comes with a plain-language gloss in parentheses (e.g. "eyebrow — the small all-caps line above a headline"). If one shows up unglossed, just ask "what's that?" — that's a bug on its side, not a gap on yours.

**Q: I can't edit code at all — what if something's wrong?**
Just describe the problem to it ("this part doesn't display fully on mobile") — you don't need to understand the code, finesse locates and fixes the issue itself.

**Q: Do I have to confirm the Design Read? Can I just have it do everything in one shot?**
You can skip it by saying "whatever you decide, just do it" — but it's not recommended. That step takes a few seconds and avoids a costly redo if the direction turns out completely wrong.

**Q: My multi-page project has drifted out of consistency — can it still be fixed?**
Yes. Say "check whether these pages are visually consistent" — finesse compares the existing pages, reverse-engineers a spec, and adjusts the pages that drifted — no need to rebuild everything.

**Q: Which tool should I use (Claude Code / Cursor / Codex / Copilot)?**
All are supported — installation steps are in the main README's "Install & tool support" section. The usage described in this document is identical across every tool.

---

## 8. One-page cheat sheet

| I want to… | I should say… |
|---|---|
| Build a new page from scratch | Describe the page type + 1-2 mood words |
| Make it more impactful | "more impact" / "too plain" |
| Tone it down | "too flashy" / "overwhelming" |
| Change the style direction | "feels off" / "not our vibe" |
| Add/reduce content density | "too sparse" / "too cluttered" |
| Add a 3D interaction | "add a 3D moment" |
| Fix just one small thing | Name the exact piece and describe the problem |
| Keep multiple pages consistent | "these pages need to share a consistent look" |
| Plug into an existing codebase | "check what design system is already in use here" |
| Do a pre-ship check | "check this page for me" / `audit` |

---

The deeper technical rules (register-detection logic, chart selection, component-system details, the specific entries in the anti-slop blacklist) live in `skills/finesse-ui/` — they're for the Skill to read, not for you to study. This checklist is all you actually need.
