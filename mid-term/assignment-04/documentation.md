# Assignment 04 — CSS Documentation

This explains every CSS concept used in `style.css` for `porfolio.html`, mapped to the assignment's requirements checklist. It was updated after a visual redesign (nav bar, hero banner, project card grid, timeline), so it reflects the current file.

## 1. Page structure at a glance

```
<nav class="site-nav">          sticky top navigation (About / Skills / Experience / Projects / Education / Contact)
<header class="hero" id="top">  full-width banner: name, tagline, intro, contact info, buttons, photo
<main class="container">        centered content column, holds all sections below
  <section id="about">          career objective + present status cards, Key Skills pill list
  <section id="skills">         technical skills as tagged cards (languages, web, database, tools...)
  <section id="experience">     professional experience as a vertical timeline
  <section id="projects">       PROJECT SHOWCASE — grid of project cards
  <section id="academic-projects"> smaller project-card grid for academic work
  <section id="education">      education history table
  <section id="achievements">   achievements checklist
  <section id="language">       language checklist
  <section id="more-info">      personal info / hobbies / references, in a card grid
<footer class="site-footer">    copyright line
```

Every original CV section is still present — nothing was deleted, only re-laid-out into cards, grids, and a timeline instead of plain paragraphs and bare lists.

## 2. What changed to make it "eye-catchy"

- **Sticky nav bar** (`.site-nav`) — jumps to any section via anchor links (`href="#projects"`, etc.).
- **Hero banner** (`.hero`) — a dark gradient header with your name, role, intro, contact details, a circular photo, and two call-to-action buttons instead of a plain table row.
- **Project showcase grid** (`#projects .projects-grid`) — each project is now an `<article class="project-card">`: a colored header band + title + description + technology tags. Cards lift and get a shadow on hover (`.project-card:hover`).
- **Skill tag pills** — both the "Key Skills" list and the technical skills section use rounded `<span class="tag">` / `<li class="skill-item">` chips instead of a plain bullet list.
- **Timeline** (`#experience .timeline`) — professional experience now reads top-to-bottom along a vertical accent line with dots, instead of a numbered list.
- **Card grids everywhere else** — About, academic projects, and "More Information" (personal info / hobbies / references) are grouped into `.about-card` / `.info-card` boxes on a CSS grid so related content sits side by side.
- **Checklist bullets** — achievements and languages use a custom checkmark (`::before { content: "\2713"; }`) instead of the default browser bullet.
- **Responsive layout** — a `@media (max-width: 800px)` block stacks the hero, nav, and grids into a single column on small screens.

## 3. Selectors used (requirement: element, class, ID)

| Type | Example in `style.css` | What it targets |
|---|---|---|
| Element selector | `body`, `h1`, `h2`, `p`, `a`, `img`, `button`, `table`, `th`, `td` | Every element of that tag, everywhere on the page |
| Class selector | `.site-nav`, `.hero`, `.section-box`, `.project-card`, `.tag`, `.skill-item`, `.timeline-item` | Only elements carrying that `class="..."` attribute |
| ID selector | `#name-heading`, `#skills-list`, `#contact-btn`, `#projects`, `#about` | One specific, unique element (IDs also double as the nav's scroll-to anchors) |

**Rule of thumb:** element selectors set broad defaults, classes style repeated groups (cards, tags, timeline items) consistently, and IDs style one unique element — or act as a jump target for `<a href="#id">`.

## 4. Required CSS properties, and where each lives now

| Property | Where it's used | Purpose |
|---|---|---|
| `background-color` | `body`, `.section-box`, `button`, `.tag`, `.hero` (via gradient) | Fills the background of an element |
| `color` | `body`, `h2`, `button`, `.tag`, `#name-heading` | Sets text color |
| `font-family` | `body`, `button` (`inherit`) | Chooses the typeface |
| `font-size` | `body`, `h1`, `h2`, `button`, `.tag` | Controls text size |
| `text-align` | `.hero`, `.intro`, `.site-footer` | Aligns text inside its container |
| `width` | `img` (150px), `.container` (1100px) | Sets an element's horizontal size |
| `height` | `img` (150px) | Sets an element's vertical size — paired with `width` so `border-radius: 50%` makes a perfect circle |
| `padding` | `.container`, `.section-box`, `button`, `th`/`td`, `.project-card-body` | Space *inside* an element |
| `margin` | `.container`, `button`, `.section-box`, `.about-card` | Space *outside* an element |
| `border` | `img`, `button`, `.section-box`, `.timeline` (left border) | Draws a line around (or beside) an element |
| `border-radius` | `img` (circle), `button`, `.section-box`, `.project-card`, `.tag` (pill shape) | Rounds corners |

The redesign also layers on `box-shadow`, CSS Grid (`display: grid`), Flexbox (`display: flex`), and `position: sticky` — these are extras on top of the required list, used to build the nav bar, hero layout, and card grids.

## 5. Hover effects

Two kinds of hover are used now:

```css
button:hover {
  background-color: #10203f;
  color: #ffffff;
  transform: translateY(-3px);
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
}

.project-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 14px 30px rgba(16, 32, 63, 0.15);
  border-color: #f5a524;
}
```

`button:hover` and `.project-card:hover` are **pseudo-class selectors** — they only apply while the mouse is over that element. `transform: translateY(...)` shifts the element upward, which combined with a bigger `box-shadow` creates a "lifting off the page" effect.

## 6. Transition (smooth hover)

```css
button {
  ...
  transition: 0.3s ease;
}

.project-card {
  ...
  transition: 0.3s ease;
}
```

`transition` is placed on the **base rule**, not on `:hover`. This tells the browser: "whenever a property on this element changes (background, transform, shadow, etc.), animate it over 0.3 seconds with an `ease` curve" — instead of snapping instantly. Because it's on the base rule, the animation plays both when the hover *starts* and when it *ends*.

- `0.3s` — duration of the animation.
- `ease` — timing function; starts slow, speeds up, ends slow (the natural-feeling default).

## 7. Quick mental model

1. **HTML** = structure/content (nav, hero, sections, cards, the button).
2. **CSS selectors** = "which elements am I styling" (element / class / ID).
3. **CSS properties** = "how do they look" (color, spacing, size, shape).
4. **Grid/Flexbox** = "how are multiple elements arranged relative to each other" (cards in rows/columns).
5. **`:hover` + `transition`** = interactivity — a state change plus an animation rule that makes it smooth instead of instant.

## 8. If your instructor asks for small changes during assessment

- **Change the color theme** → edit the hex codes at the top of `style.css` (`#10203f` is the dark navy used everywhere, `#f5a524` is the gold accent).
- **Change fonts** → edit `font-family` on `body`.
- **Add another skill pill** → add another `<li class="skill-item">...</li>` inside `<ul id="skills-list">`.
- **Add a new project card** → copy one `<article class="project-card">...</article>` block inside `.projects-grid` in `porfolio.html` and edit its title/description/tags.
- **Add a nav link** → add an `<li><a href="#your-section-id">Label</a></li>` inside `.nav-links`, and make sure a `<section id="your-section-id">` exists to jump to.
- **Rename/change a button** → edit text inside `<button id="contact-btn">...</button>`; to make it link somewhere, wrap it in an `<a>` or add an `onclick`.
- **Adjust spacing** → tweak `padding` (inside) vs `margin` (outside) on `.section-box`, `.project-card-body`, or `.container`.
- **Change grid columns** → edit `grid-template-columns` in `.projects-grid`, `.skills-grid`, `.about-grid`, or `.info-grid` (e.g. `minmax(280px, 1fr)` controls the minimum card width before wrapping).
