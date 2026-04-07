# Jinyeop Song — Personal Site

## Architecture

- **Jekyll 4.3** + **Hydejack 9.1 theme** (Ruby 3.2.8)
- Blog posts: `_posts/YYYY-MM-DD-slug.md` (Markdown + front matter)
- Pages: `about.md`, `cv.md`, `publications.md`, `posts.md`
- Custom SCSS: `_sass/my-style.scss` (blog styling, callout boxes)
- Template injections: `_includes/my-head.html`, `_includes/my-body.html`

## Project Pages (Top-Level HTML)

The site has **self-contained project pages** at the root — these are standalone HTML files (not Jekyll-templated) with inline CSS:

- `protein-llm.html` — Protein LLM series (teal accent: `#4fb1ba`)
- `autoresearch-denovo.html` — Autoresearch De Novo (orange accent: `#e8704a`)

These are linked from `_config.yml` under `menu:`.

### Adding a New Project Page

Follow these rules exactly:

1. **Copy the template**: Use `protein-llm.html` or `autoresearch-denovo.html` as the starting point.

2. **Shared stylesheet**: All project pages use `assets/css/project-page.css`. Link it in the `<head>`:
   ```html
   <link rel="stylesheet" href="/assets/css/project-page.css">
   ```
   The dark theme palette is defined via CSS variables in the shared stylesheet. **Do not duplicate these styles inline.**

3. **Choose an accent color** and override the CSS variables in a small inline `<style>` block:
   ```html
   <style>
     :root {
       --accent: #e8704a;           /* main accent */
       --accent-hover: #f0956e;     /* hover brightened */
       --accent-bg: rgba(232, 112, 74, 0.1);      /* sidebar hover bg */
       --accent-bg-active: rgba(232, 112, 74, 0.15); /* sidebar active bg */
       --thesis-gradient-end: #d35400;  /* thesis box gradient */
     }
   </style>
   ```
   The default accent (teal `#4fb1ba`) requires no overrides — just link the CSS.

   Existing accents:
   - Protein LLM: teal `#4fb1ba` (default, no override needed)
   - Autoresearch De Novo: orange `#e8704a`

4. **Top navigation**: Show project title, not Publications/CV/Blog:
   ```html
   <nav class="topnav">
     <button class="menu-toggle" ...>&#9776;</button>
     <a href="/" class="brand">Jinyeop Song</a>
     <span class="nav-title">Project Name Here</span>
   </nav>
   ```

5. **Sidebar structure**:
   - `<a href="/posts/" class="back-link">← Back to Blog</a>` at top
   - Overview sections first (primary navigation)
   - Supplementary/deep-dive sections below a `.sidebar-divider`
   - External links and reports at the bottom

6. **SVG architecture diagram** (add in the overview section):
   - Background: `#151520`
   - Rounded corners: `rx="7"` for boxes, `border-radius:10px` on container
   - Arrow markers: solid (`rgba(255,255,255,.5)`) and dashed (`rgba(255,255,255,.3)`)
   - Column headers: uppercase, letter-spacing 2.5, fill `.5` opacity
   - Arrow labels: italic, fill `.5` opacity (never below `.4`)
   - Box text: title at `font-weight="700"`, subtitle at `.55-.6` opacity
   - Group borders: dashed `stroke="rgba(255,255,255,.1)"`
   - Training/pipeline section at bottom with horizontal flow
   - Legend at very bottom

7. **Required CSS classes** (include all for parity):
   - `.central-thesis`, `.callout`, `.finding`, `.conclusion` (box types)
   - `.pillars`, `.pillar` (grid cards)
   - `.part-section`, `.part-label`, `.part-date` (section dividers)
   - `.winner`, `.loser` (table semantic highlighting)
   - `.fig`, `.figcaption` (images)
   - `.resources` (resource link boxes)

8. **Register in `_config.yml`** under `menu:`:
   ```yaml
   - title:             Project Name
     url:               /project-name.html
   ```

9. **Reports subdirectory**: Detailed HTML reports go in `reports/` and are linked from the sidebar.

## Development

```bash
bundle install
bundle exec jekyll serve    # http://localhost:4000
```

Project pages (standalone HTML) can be previewed directly in a browser or with `python3 -m http.server`.
