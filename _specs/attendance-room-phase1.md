---
status: COMPLETE
brief-from: Luna 3.0
date: 2026-08-06
built-by: Luna Tech
commits: 62fff64 (phase 1 shell)
---

# Spec: Attendance Room — Phase 1 Shell

**Status: COMPLETE. All three items are live in the repo. This document records what was built and serves as the pattern reference for Phase 2 and future attendance room specs.**

Factor pages are NOT in scope here — see Phase 2 spec when cleared.

---

## Context Codex needs

- Repo: `PenelopeMudd/HecKte`, served at `penelopemudd.github.io/HecKte/`
- SchoolHouse lives at `schoolhouse/` — all paths below are repo-root-relative
- Inline CSS only — no external stylesheet on landing or territory pages
- Token system: `--ground` (bg), `--ink` (text), `--muted` (secondary), `--amber` (accent/eyebrow), `--border` (rule)
- Light values: `--ground:#F5F0E8; --ink:#1B3A4B; --muted:rgba(27,58,75,0.55); --amber:#C4883A; --border:rgba(27,58,75,0.15)`
- Dark values: `--ground:#1E1B16; --ink:#E4D9CC; --muted:rgba(228,217,204,0.55); --amber:#D09652; --border:rgba(228,217,204,0.14)`
- Dark mode via `@media(prefers-color-scheme:dark)` + `:root[data-theme="dark"]` / `:root[data-theme="light"]` overrides
- Every page must include `<meta name="color-scheme" content="light dark">` and `color-scheme:light dark;` inside `:root` CSS
- Typography: `font-family: Georgia, 'Times New Roman', serif` for body; `-apple-system, Arial, sans-serif` for labels/eyebrows/nav
- Max-width: `720px`, centered, `padding: 3rem 1.5rem 5rem`

---

## File 1: `schoolhouse/index.html` — Attendance door

**Status: COMPLETE** (live, links to `attendance.html`, eyebrow "Missouri DESE · Standard 5")

### What was built

The Attendance door was activated and added between the Classroom Management door and the Browse group. Pattern to match for future doors:

```html
<div class="door">
  <p class="door-eyebrow">Missouri DESE &middot; Standard 5</p>
  <a class="door-title" href="attendance.html">Attendance</a>
  <p class="door-desc">Attendance is a territory &mdash; conditions, not a single behavior. Nine factors, mapped from what&rsquo;s established to what&rsquo;s emerging.</p>
</div>
```

### CSS classes in use on this page

- `.door` — `border-top: 2px solid var(--ink); padding: 1.25rem 0 1.75rem`
- `.door-eyebrow` — `font-size:0.7rem; letter-spacing:0.08em; text-transform:uppercase; color:var(--amber)`
- `.door-title` — `font-size:1.15rem; font-weight:normal; color:var(--ink); text-decoration:none; display:block`
- `.door-title.disabled` — `color:var(--muted); pointer-events:none` (greyed/Coming state)
- `.door-desc` — `font-size:0.88rem; color:var(--muted); margin-top:0.4rem; line-height:1.6`
- `.browse-group` — `margin-top:2.5rem` (wrapper for Browse/About doors at bottom)

---

## File 2: `schoolhouse/attendance/index.html` — Territory room entry

**Status: COMPLETE (shell live) — FACTOR NAMES NEED UPDATING before Phase 2**

### Factor name mismatch — action required in Phase 2

The shell was built with the brief's original factor names. The actual factor HTML pages use PhD 2.0 names. These must match before any factor door is activated.

| Current name in index.html | Actual factor page filename |
|---------------------------|-----------------------------|
| Poverty & Economic Instability | factor-3-basic-needs.html |
| Housing Instability | (no direct match — absorbed into factor-3 and factor-4) |
| Transportation | factor-2-transportation-access.html |
| Health Access | factor-1-physical-health.html |
| School Climate | factor-6-school-climate-safety.html |
| Chronic Health Conditions | (absorbed into factor-1) |
| Family Engagement | factor-4-family-capacity.html |
| Mental Health | factor-5-mental-behavioral-health.html |
| Mobility & Enrollment Instability | (no direct match) |

PhD 2.0 factor names (use these in Phase 2 index update):
1. Physical Health → `factor-1-physical-health.html`
2. Transportation & Access → `factor-2-transportation-access.html`
3. Basic Needs & Economic Stability → `factor-3-basic-needs.html`
4. Family Capacity & Caregiving → `factor-4-family-capacity.html`
5. Mental & Behavioral Health → `factor-5-mental-behavioral-health.html`
6. School Climate & Safety → `factor-6-school-climate-safety.html`
7. Relationships & Belonging → `factor-7-relationships-belonging.html`
8. Academic Experience → `factor-8-academic-experience.html`
9. Meaning, Identity & Value → `factor-9-meaning-identity-value.html`

### What was built (current HTML structure)

Page head — every inline-CSS territory page uses this pattern:
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="color-scheme" content="light dark">
  <title>[Page title] — SchoolHouse</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    :root {
      color-scheme: light dark;
      --ground: #F5F0E8;
      --ink: #1B3A4B;
      --muted: rgba(27,58,75,0.55);
      --amber: #C4883A;
      --border: rgba(27,58,75,0.15);
    }
    @media (prefers-color-scheme: dark) {
      :root {
        --ground: #1E1B16;
        --ink: #E4D9CC;
        --muted: rgba(228,217,204,0.55);
        --amber: #D09652;
        --border: rgba(228,217,204,0.14);
      }
    }
    :root[data-theme="dark"] {
      --ground: #1E1B16; --ink: #E4D9CC;
      --muted: rgba(228,217,204,0.55); --amber: #D09652;
      --border: rgba(228,217,204,0.14);
    }
    :root[data-theme="light"] {
      --ground: #F5F0E8; --ink: #1B3A4B;
      --muted: rgba(27,58,75,0.55); --amber: #C4883A;
      --border: rgba(27,58,75,0.15);
    }
    /* ... page-specific rules ... */
  </style>
</head>
```

Page body structure:
```html
<body>
  <a class="back-link" href="../">&larr; SchoolHouse</a>

  <p class="eyebrow">Missouri DESE &middot; Standard 5</p>
  <h1>Attendance</h1>
  <p class="standfirst">[1–2 sentence orientation. Not instruction — territory.]
  Attendance is a territory &mdash; a set of conditions, not a single behavior.
  This room maps what we know, what&rsquo;s emerging, and what remains open.</p>

  <div class="factor-list">
    <!-- 9 doors, all disabled/Coming until factor pages are cleared -->
    <div class="door">
      <span class="door-title disabled">[Factor name]</span><span class="pill">Coming</span>
    </div>
    <!-- repeat x9 -->
  </div>

  <a class="resource-link" href="resources/">&rarr; Attendance Resource Room</a>

  <footer>SchoolHouse &nbsp;&middot;&nbsp; an unreliable translator</footer>
</body>
```

CSS classes specific to territory room:
- `.eyebrow` — `font-family:-apple-system,Arial,sans-serif; font-size:0.7rem; letter-spacing:0.08em; text-transform:uppercase; color:var(--amber); margin-bottom:0.35rem`
- `.back-link` — `font-family:-apple-system,Arial,sans-serif; font-size:0.72rem; letter-spacing:0.1em; text-transform:uppercase; color:var(--muted); text-decoration:none; display:inline-block; margin-bottom:2rem`
- `.standfirst` — `font-size:1rem; color:var(--muted); margin-bottom:3rem; line-height:1.7`
- `.door` — `border-top:1px solid var(--border); padding:1rem 0 1.25rem`
- `.door-title` — active state: `font-size:1.05rem; font-weight:normal; color:var(--ink); text-decoration:none; display:inline`
- `.door-title.disabled` — `color:var(--muted); pointer-events:none`
- `.pill` — `display:inline-block; font-family:-apple-system,Arial,sans-serif; font-size:0.58rem; letter-spacing:0.07em; text-transform:uppercase; color:var(--muted); border:1px solid var(--border); padding:0.1rem 0.45rem; margin-left:0.55rem; vertical-align:middle`
- `.resource-link` — `display:block; margin-top:2.5rem; padding-top:1.5rem; border-top:1px solid var(--border); font-family:-apple-system,Arial,sans-serif; font-size:0.82rem; color:var(--muted); text-decoration:none`

---

## File 3: `schoolhouse/attendance/resources/index.html` — Resource room shell

**Status: COMPLETE (shell live, no sources yet)**

### What was built

Minimal shell. Sources added as factor articles are built and cleared.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="color-scheme" content="light dark">
  <title>Attendance — Resource Room — SchoolHouse</title>
  <!-- [same :root token block as above] -->
</head>
<body>
  <a class="back-link" href="../">&larr; Attendance</a>
  <h1>Attendance &mdash; Resource Room</h1>
  <p class="standfirst">Sources used across Attendance articles. Each claim links here;
  scope and standing are noted at the point of claim.</p>
  <p class="placeholder">Sources added as articles are built.</p>
  <footer>SchoolHouse &nbsp;&middot;&nbsp; an unreliable translator</footer>
</body>
</html>
```

---

## Phase 2 prerequisites (do NOT build until cleared)

1. Update `attendance/index.html` factor list — replace 9 original names with PhD 2.0 names (table above)
2. Each factor door activates only when its factor page is cleared by PhD + HCD
3. PhD 2.0 Physical Health page is built and live (Luna Tech, 2026-08-06) — awaiting HCD review before door activates

---

## Pattern notes for future specs

- Territory room = orientation only, no instruction. 1–2 sentence standfirst, factor list, resource room link, footer.
- Factor room = full content page using `factor.css` (see `schoolhouse/attendance/factor.css`). Different structure — see factor page files for pattern.
- Resource room = source list. Shell first, sources added as articles clear.
- Commit each file separately if doing multiple in one session — easier to revert.
- Append to `.claude/tech-ships-log.md` immediately after each push.
- Post to `.claude/tech-results-queue.md` so CC and HCD know what landed.
