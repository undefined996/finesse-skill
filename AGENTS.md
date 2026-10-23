# finesse — Agent Instructions

> **For OpenAI Codex and other agent runtimes that read `AGENTS.md`.**
> The full skill is at `skills/finesse-ui/SKILL.md`. Deep reference material lives in `skills/finesse-ui/references/`. Load what you need per phase — do not inline everything at once.

---

## Apple design language

For Apple / 苹果风 requests, read `skills/finesse-ui/references/apple-design.md` before choosing the substrate. Keep the register and add `design-language=apple` plus `apple-mode=editorial|app|spatial`. The scoped aesthetic overrides there supersede conflicting defaults in this file. Editorial recipes and seven portable interactive studies are indexed in `skills/finesse-ui/references/apple-patterns.md`. Reuse `interaction-motion.md` for gestures; app and spatial do not automatically mean Bento or glass everywhere.

## What finesse does

finesse builds interfaces routed by **register**:

- **brand** — landing pages, brand sites, launches, portfolios, hero pages. Design IS the product. Optimize for spectacle + soul + first impression. Uses a real visual engine (Three.js / Canvas / GLSL / GSAP).
- **product** — dashboards, admin panels, analytics, data tables, app shells, settings. Design SERVES the product. Optimize for clarity + density + usability.
- **commerce** — PDP, PLP, cart, checkout. A hybrid: route to brand or product by what the specific page is doing.
- **h5** — pages that only ever live on a phone: H5 / 移动端页面 / 活动页 / mini-program screens / app prototypes / mobile PDPs. A **container** register — it fixes the phone frame, safe areas, thumb zone and native furniture, then wraps one of the three above for content. A mobile PDP is `h5` + `commerce`.

All share the same premium substrate and anti-slop blacklist. None is allowed to look cheap.

---

## Commands (targeted iteration)

A full build runs the whole workflow below. For iterating on an existing page, route the request through one verb instead of rebuilding — Codex has no slash commands, so map the user's intent to the verb and load only that reference.

| Verb | Intent it matches | Load |
|------|-------------------|------|
| `craft` | "build me a landing page / dashboard" (default) | full workflow |
| `init` | "set up finesse / new project" → write `PRODUCT.md` brief | `references/init.md` |
| `document` | "capture / document the design system" → extract `design-model.yaml` | `references/document.md` |
| `audit` | "is this any good?", "review it" — **read-only**, never edits | `references/audit.md` (runs `scripts/detect.mjs`) |
| `bolder` | "too plain / boring" → SPECTACLE +2, engine up a tier | `references/hero-engines.md` |
| `quieter` | "too flashy / janky" → SPECTACLE −2, engine down a tier | `references/hero-engines.md` |
| `soul` | "wrong vibe *for this page*" → re-compose the soul, re-lock color | `references/style-personas.md` |
| `diverge` | "**every page looks the same** / feels generic / 每次都差不多" → systemic anti-sameness: recompose from 5 orthogonal axes, two-altitude anti-default, break the argmax, check the used-list | `references/divergence.md` |
| `animate` | "make it move / different animation" → add/swap engine only | `references/hero-engines.md` |
| `depth` | "add depth / make it 3D / tilt / parallax" → add one 3D moment (CSS pseudo-3D, or Three.js for a real object) | `references/3d-effects.md` |
| `densify` | "too sparse / too dense" → DENSITY ± | `references/product-ui.md` |
| `redesign` | "improve / fix this page" → audit-first, never full-rebuild | `references/redesign-mode.md` |

For a single complaint, change **one** thing, keep the substrate and soul, then re-run the relevant pre-flight gates.

---

## Mandatory workflow (execute in order)

### 1. Design Read — before any code
If a `PRODUCT.md` exists at the project root, read it first — it's the locked brief (register, soul, dials, anti-references) and overrides your guesses; read `design-model.yaml` too if present (locked palette/type/substrate). Missing on a multi-page/repeat project? Offer `init` (and `document` for existing code) before generating.

Read the brief. Determine the register. Output exactly one line:

```
Design Read: {industry} · {soul in 2–3 words} · register={brand|product} · SPECTACLE={1–10} · hero-engine={type or "none"}
```

Then name the lazy default aesthetic for this brief and state how you are beating it.

### 2. Set the three dials
- **SOUL** (1–10): how opinionated/branded the personality is
- **SPECTACLE** (1–10): how technically-ambitious the visual engine is
- **DENSITY** (1–10): information per viewport

Product register: pin SPECTACLE ≤ 4, DENSITY ≥ 6.

If SPECTACLE ≥ 7, you MUST ship a working engine. A gradient blob at SPECTACLE 8 is broken. Drop to 4 and ship a polished static page instead.

### 3. Lay the substrate for the selected register
Brand defaults follow `skills/finesse-ui/references/design-dna.md`; product uses `product-ui.md` §0 and does not inherit grain, vignette or giant display type. Apple language uses the scoped overrides above. Brand defaults:
- SVG grain layer (`feTurbulence`, `opacity .025–.05`)
- Radial-gradient vignette on dark heroes
- Display headings: `clamp()` size, negative tracking (`-.02 to -.045em`), `line-height .86–.95`, extreme weight contrast
- Translucent borders (`rgba(255,255,255,.07–.22)` dark / `rgba(0,0,0,.06–.08)` light)
- No pure `#fff` / `#000` — tint toward brand hue
- Color lock: one accent owns the whole page

### 4. Fork by register

**brand path:**
- Pick a soul persona from `skills/finesse-ui/references/style-personas.md`
- Build one hero engine from `skills/finesse-ui/references/hero-engines.md`
- `prefers-reduced-motion` fallback is mandatory

**product path:**
- Build component system + data viz per `skills/finesse-ui/references/product-ui.md`
- Skip soul personas and hero engines

**h5 path:**
- Read `skills/finesse-ui/references/h5-mobile.md` **before** any layout decision — the frame goes up first
- Build the frame (§1): viewport contract, locked `body` + scrolling container, the 560px desktop phone frame, safe-area math (§2)
- Pick one of six morphologies (§4), then load the content register it wraps and follow that path above
- Furniture comes from §5's recipes, not from invention (§11 — diverge on the soul, never on where the back button is)
- Run §10's gates instead of the mobile floor

### 5. Run the cheapness blacklist
Run the local detector first (no network, pure file scan), then add your own eye:

```
node skills/finesse-ui/scripts/detect.mjs --json <target ...>
```

It reports findings P0/P1/P2 with `file:line`, a `p0` count, and a `notCovered[]` list of tells it can't see. It **always exits 0** (findings are data in the JSON, not a tool failure — read `p0`; `--strict` makes a P0 block with a non-zero exit for CI). A clean run means "no regex-detectable slop", not "good page" — always continue into the by-hand pass. If the script is absent, scan by hand; don't treat its absence as a pass. Hard bans:
- Em-dashes in copy as a flourish (most-violated AI tell — zero exceptions)
- Gradient text, default glassmorphism, AI-purple glow, side-stripe card borders
- Eyebrow label on every section; numbered `01 · 02 · 03` section markers
- Identical 6-card grids (icon + title + text × 6)
- Fake-precise numbers (`92%`, `4.1×`) with no source
- Default-category palettes reached for without reason
- Zero imagery on image-implied briefs

### 6. Pre-flight before declaring done
See `skills/finesse-ui/references/preflight.md`. Run `node skills/finesse-ui/scripts/detect.mjs --json <target>` and confirm `p0` is 0 (the script always exits 0; the count lives in the JSON), and when a browser is available, open the page and screenshot the hero to confirm the engine renders real pixels (not a white/flat screen). Mandatory gates:
- [ ] Design Read output + dials documented
- [ ] Correct register/language substrate applied; grain/vignette are not universal gates
- [ ] SPECTACLE claimed = SPECTACLE shipped (detector + browser-verified, not just asserted)
- [ ] Cheapness blacklist cleared
- [ ] `prefers-reduced-motion` handled on every animation
- [ ] WCAG AA contrast: body ≥ 4.5:1, large text ≥ 3:1
- [ ] Layout families diversified (no repeated pattern dominance)
- [ ] Mobile layout declared per multi-column section

If any gate fails: fix it. Do not ship and note it as a known issue.

---

## Reference files

| File | Load when |
|------|-----------|
| `skills/finesse-ui/references/divergence.md` | **At §0, before the Design Read.** Output keeps converging / "feels generic" / "every page looks the same". Compose the soul from 5 orthogonal axes instead of picking off a persona list; two-altitude anti-default; break the model's argmax with a die roll; the used-list that makes "don't repeat" executable; assert-then-confirm (never a text menu of adjectives). **Read its §0 register boundary first** — divergence is a goal for brand, a *bounded* tactic for product (never diverge on dashboard nav conventions) |
| `skills/finesse-ui/references/design-dna.md` | Implementing the substrate layer |
| `skills/finesse-ui/references/hero-engines.md` | Building a brand hero engine (the decision layer: which engine, and hero-only vs full-page scope) |
| `skills/finesse-ui/references/page-crafting.md` | **The brand implementation layer** (what `chart-crafting.md` is to `dataviz.md`) — when you stop choosing and start writing: the motion gate (`REDUCE`/`FINE` + terminal states; **universal, product too**), canvas DPR + cyclic palettes + Gaussian envelopes, `mask-image` photo dissolve, photographic-hero scrim stack, container-query panels, nav scroll-spy over alternating sections, zero-dependency sticky horizontal pin, exploded-view scrub, colorway pin+snap, `clip-path` wipes, hand-written FLIP lightbox, generative (guillotine-split) layouts, CSS-only geometric collage, full-page engine + section scrims, Fibonacci→KNN→traversal 3D |
| `skills/finesse-ui/references/3d-effects.md` | Adding a 3D moment: CSS tilt/flip/coverflow/parallax or Three.js model/displacement |
| `skills/finesse-ui/references/style-personas.md` | Choosing a brand soul/persona |
| `skills/finesse-ui/references/inspiration-catalog.md` | Wider bench of real pages per persona, or a brief that doesn't fit any of the 10 personas |
| `skills/finesse-ui/references/anti-cheap.md` | Running the cheapness audit |
| `skills/finesse-ui/references/audit.md` | Read-only diagnostic (cheapness + spectacle + pre-flight) |
| `skills/finesse-ui/references/product-ui.md` | Product register: dashboards, tables, charts |
| `skills/finesse-ui/references/ai-console.md` | **AI 工作台 / agent console / copilot UI — the third product sub-type: a page you *delegate on*.** A dashboard fails by being unreadable, a wizard by being unfinishable; this one fails by being **untrustworthy**. Carries the three tenses on one screen (queue · live run · history), the **run stream** that replaces the chart as the centrepiece, the **nine run states** (`product-ui.md` §5's eight component states don't cover `partial` / `stopped` / `awaiting-input`), stop as a resident primary control, the in-stream approval card with linked evidence, cost as a receipt line, the artifact surface, the desktop three-column shell, and what changes on a phone (§9). Example: `examples/relay-agent-console.html` |
| `skills/finesse-ui/references/dataviz.md` | Chart-heavy UI beyond the starter table: full 25-type matrix, a11y grade + fallback, library picks (the decision layer) |
| `skills/finesse-ui/references/chart-crafting.md` | Hand-building charts in a single self-contained file — no-library SVG+GSAP recipes: coordinate normalization, line/area draw-in, donut/gauge grow, stacked bars, sparklines, reduced-motion pairing (the implementation layer) |
| `skills/finesse-ui/references/theming.md` | Brief asks for a light/dark toggle or swappable named themes |
| `skills/finesse-ui/references/commerce-ui.md` | Commerce register: PDP, PLP, cart, checkout, dark-pattern blacklist |
| `skills/finesse-ui/references/h5-mobile.md` | **h5 register — the page only ever lives on a phone.** Load it *before* any layout decision: the viewport contract, the locked-`body`/scrolling-container inversion, the 560px desktop phone frame, `env(safe-area-inset-*)` math, the thumb-zone inversion (primary actions at the **bottom**), touch rules with no desktop equivalent (`passive`, `pointercancel`, tap-highlight, 44px), six phone morphologies, and the native furniture recipes — status bar, TabBar, bottom sheet, FAB, push and hand-written FLIP transitions. **Not `mobile-floor.md`**: that keeps a desktop page from breaking on a phone; this is for a page with no desktop form at all |
| `skills/finesse-ui/references/asset-sourcing.md` | No real imagery on hand: generate vs. real stock vs. placeholder fallback, with the authorization step for each |
| `skills/finesse-ui/references/preflight.md` | Pre-flight checklist |
| `skills/finesse-ui/references/redesign-mode.md` | Upgrading an existing page, audit-first |
| `skills/finesse-ui/references/design-model.md` | Multi-page token consistency |
| `skills/finesse-ui/references/init.md` | New project: write `PRODUCT.md` brief |
| `skills/finesse-ui/references/document.md` | Existing code: extract `design-model.yaml` |
| `skills/finesse-ui/scripts/detect.mjs` | Local slop + spectacle detector (run in audit / pre-flight) |

---

## Out of scope

Pure backend / API / data tasks with no UI. Briefs that explicitly require generic, zero-craft output (finesse always brings craft — if the user wants bland, that is a different tool).
