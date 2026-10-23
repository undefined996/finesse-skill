# Copilot Instructions: finesse Design Standard

> GitHub Copilot reads this file automatically. These rules replace generic AI design defaults with finesse's never-cheap, high-craft standards.

## Apple design language

For Apple / 苹果风 requests, first read `skills/finesse-ui/references/apple-design.md`. Retain the register and choose editorial, app or spatial mode. Its scoped overrides supersede conflicting aesthetic defaults below: deliberate black/white surfaces and clean editorial layouts are allowed; grain, vignette, a hero engine and glass are not automatic requirements. Keep accessibility and functional gates. Use `apple-patterns.md` for the seven bundled card studies and `interaction-motion.md` for gestures.

## Core Directive

You are generating UI for a finesse project. finesse routes by **register**:
- **brand** (landing pages, hero sites, portfolios) — spectacle + soul + first impression
- **product** (dashboards, analytics, admin) — clarity + density + usability
- **commerce** (PDP, PLP, cart, checkout) — a hybrid; route to one of the two above by what the page does
- **h5** (H5 / 移动端页面 / 活动页 / app 原型 / mobile PDP) — a page that only ever lives on a phone. A **container** register: fix the frame first, then wrap one of the three above. See rule 9.

All are **never cheap**. The premium substrate and anti-slop rules apply to all.

## The 9 Non-Negotiables

1. **Read the brief first, and assert a direction the user can actually veto.** Before any code, output `Design Read: {industry} · {soul} · register={brand|product|commerce|h5} · SPECTACLE={n}`, then — on its own line — **`You'll see:` a plain description of what renders** (color, whether anything moves, type size, structure; no jargon, no library names), then **two named likely objections** (`Not right? Most likely: ① … ② …`). Stop and wait. The coordinate line is for you; `You'll see:` is the only line a non-designer can answer, and a gate only "go ahead" can pass is not a gate. Also name the lazy default aesthetic and how you are beating it — at **two altitudes**: the category default ("coffee → beige+brass") *and* the obvious anti-reference ("AI tool that's not SaaS-cream → editorial-typographic"). Avoiding the first reflex but landing on the second is still slop.
   - **Before saying "done," check the built page against that `You'll see:` line clause by clause.** Anything that quietly became something else (a moving hero degraded to a static image, a dark theme drifting light) is a P0 — every other rule can pass while the page stops being what the user approved.
   - **Name the image slots in that same block, and then wait.** Add an **`Images:`** line: how many pictures the page wants, what each depicts, and where they would come from **in this session** (check your actual tools first — image-gen available? network fetch only? neither?). Judge the slots off the **skeleton, not the industry** — a hero, a gallery, a PDP shot, an H5 cover or scene, even a dashboard's empty state or avatar row. Food/hotel/fashion briefs are the obvious cases, not the boundary; if the page truly wants none, write `none` and one clause of why. **This is an offer the user answers — never a licence to act on it.** Do not generate images and do not download or hotlink stock because you judged the brief implied them: both spend the user's budget or pull from the open network, and only an explicit yes to *this* question authorizes either. Silence, or approval of something else, is a no. Protocol: `skills/finesse-ui/references/asset-sourcing.md`.
   - **Explain in observable terms, always.** Gloss any term the user didn't use first — *eyebrow (the small all-caps line above a headline)*, *grain (a nearly invisible speckle so flat color doesn't read plastic)*. Never emit internal bookkeeping (five-axis coordinates, `differs on E + C + A`, reference filenames).

2. **Premium substrate on every page.** SVG grain layer (`feTurbulence`, `opacity .025–.05`). Radial vignette on dark heroes. Display headings with negative tracking (`-.02 to -.045em`) and `line-height .86–.95`. Translucent borders, never `rgba(0,0,0,1)` lines. No pure `#fff`/`#000`.

3. **SPECTACLE claimed = SPECTACLE shipped.** If you say Three.js, ship Three.js. If the engine is out of scope, drop to 4 and ship a polished static page. Never half-build something that janks.

4. **Em-dash ban. No exceptions.** The single most-violated AI tell. Replace with a comma, period, or restructure the sentence.

5. **No eyebrow on every section.** The tiny uppercase tracked label above every headline is the #1 layout tell. Max 1 eyebrow per 3 sections. The headline usually suffices alone.

6. **Color lock.** One accent owns the whole page. No surprise teal badge on a rose page. Audit every component before shipping.

7. **`prefers-reduced-motion` is mandatory.** Freeze canvas loops, freeze grain animation, provide a static fallback. Never ship motion with no escape hatch.

8. **Complete implementation only.** No `// TODO: implement`, no placeholder text, no stubbed components. Write the full, working code every time.

9. **H5 pages get the frame before anything else.** If the page only ever opens on a phone, do not write a responsive layout and squeeze it — build `skills/finesse-ui/references/h5-mobile.md` §1 first. The five things that are wrong by default: `<meta viewport>` needs `viewport-fit=cover` or `env()` silently returns `0px`; **`body` is locked (`overflow:hidden`) and a child scrolls**, the inverse of every other register; `env(safe-area-inset-*)` must appear on the status bar, the bottom bar, sheets, **and** the scroll container's bottom padding, or the last row hides under the TabBar forever; primary actions go to the **bottom** (thumb reach), never top-right; every tappable thing needs `-webkit-tap-highlight-color: transparent`, a `:active` state, and a ≥44px hit area, because hover does not exist. Ship the desktop phone frame at `@media (min-width: 560px)`.

10. **An AI 工作台 is not a chat window.** If something other than the user does the work over a duration — an agent runs multi-step tasks, output streams in, a run can fail halfway — the page must answer four questions continuously: what is it doing right now, why did it do that, what did it cost, and how do I stop it. So: a **run stream** (one row per step, with the tool name, its object, and a duration; expandable to the verbatim payload) instead of one spinner; **failed steps expanded by default** with retry-from-this-step; a `partial` state that is never rendered green; **停止 as a resident primary control**, never behind a hover or a menu, repainting within one frame and naming the step it died on; and an **approval card inside the stream** (what it will do / what it affects / the evidence, linked / approve · edit · reject) rather than a modal. Full spec: `skills/finesse-ui/references/ai-console.md`. Palette: reject the AI-violet default, and make "waiting on you" louder than "handled automatically".

## Hard Bans

- Gradient text, default glassmorphism, AI-purple glow, side-stripe card borders
- Numbered `01 · 02 · 03` section markers as default architecture
- Identical 6-card grids (icon + title + description × 6)
- Fake-precise numbers (`92%`, `4.1×`) without a real source
- Default-category palettes (beige+brass for craft, purple-glow for AI/SaaS) reached for without reason
- A gradient blob filling a slot that wanted a photograph — **and its mirror,** images that appeared on the page without the user ever saying yes to them
- **h5 only:** a desktop layout squeezed into 406px; a visible scrollbar inside the phone frame; a hardcoded `9:41` status bar; a bottom bar covering the last content row; `position: fixed` for the TabBar instead of `absolute` inside the frame

## Iterating on an existing page

Don't rebuild for a single complaint — route to one verb and adjust only that: `audit` (read-only review), `bolder` / `quieter` (SPECTACLE ±), `soul` (re-pick persona), `animate` (engine only), `depth` (add one 3D moment — CSS tilt/flip/coverflow/parallax, Three.js for a real object), `densify` (DENSITY ±), `redesign` (audit-first fix). See `skills/finesse-ui/SKILL.md` → Commands.

## Reference Material

The full skill lives in `skills/finesse-ui/SKILL.md`. Deep material in `skills/finesse-ui/references/` (incl. `audit.md` for read-only diagnostics). Load what you need per phase. Inside the finesse repo, `node skills/finesse-ui/scripts/detect.mjs --json <target>` scans for slop and spectacle-claimed-not-shown.
