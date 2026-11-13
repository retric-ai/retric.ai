# retric.ai

Source for [retric.ai](https://retric.ai): a static site with no build step (plain HTML, CSS and SVG, with a little optional JavaScript),
deployed to GitHub Pages by `.github/workflows/pages.yml` on every push to `main`.

## Local preview

```bash
python3 -m http.server 8000   # then open http://localhost:8000
```

## One-time setup

1. **Repository settings → Pages → Build and deployment → Source:** select **GitHub Actions**.
2. **Organization settings → Pages → Verified domains:** add `retric.ai` and create the TXT
   record GitHub shows you (`_github-pages-challenge-retric-ai.retric.ai`). This stops other accounts from claiming the domain.
3. **DNS at your registrar**:

   | Type  | Host  | Value |
   |-------|-------|-------|
   | A     | `@`   | `185.199.108.153` |
   | A     | `@`   | `185.199.109.153` |
   | A     | `@`   | `185.199.110.153` |
   | A     | `@`   | `185.199.111.153` |
   | AAAA  | `@`   | `2606:50c0:8000::153` |
   | AAAA  | `@`   | `2606:50c0:8001::153` |
   | AAAA  | `@`   | `2606:50c0:8002::153` |
   | AAAA  | `@`   | `2606:50c0:8003::153` |
   | CNAME | `www` | `retric-ai.github.io` |

   Many `.ai` registrars support ALIAS/ANAME records at the apex; the A/AAAA records above work everywhere.
4. **Repository settings → Pages → Custom domain:** enter `retric.ai` (the `CNAME` file in this repo
   also holds it), wait for the DNS check, then tick **Enforce HTTPS**.

## Structure

```text
index.html                  single-page site
404.html                    not-found page
assets/tokens.css           design tokens, copied from devops-cli src/devops_cli/design/ (do not edit the copied blocks), then the site tokens
assets/site.css             styles: every color, font, space and radius comes from tokens.css (light/dark via prefers-color-scheme)
assets/favicon.svg          logo mark
.github/workflows/pages.yml GitHub Pages deployment
.nojekyll                   stops a Jekyll build if Pages publishes from a branch (the Actions deploy has no Jekyll step)
CNAME                       custom domain for GitHub Pages
robots.txt                  crawler rules
sitemap.xml                 sitemap
```

## Design

The page uses the Retric design tokens (`assets/tokens.css`) and the faces Source Sans 3, Source Serif 4 and
Source Code Pro (SIL OFL) from Google Fonts, with the fallback stacks of the tokens. The look is "early web,
rebuilt": 80s and 90s computer and hacker culture redrawn as vector art. The cards are 90s desktop windows with
1 px bevels and no shadows. The section labels are shell commands and a man-page header. The contact terminal
plays a modem handshake, the footer has a webring, 88x31 buttons, a hang-up line and a static `uptime` line,
and the 404 page dials the missing path and gets `NO CARRIER`.

`color.accent` (petrol teal) is the main accent: links, buttons, focus and the circuit traces. The site token
`site.secondary` (P3 amber) is the secondary color: the background and wireframe grids (`site.grid`), the
header and footer rules, the dashed section partitions and the webring frame (`site.rule`). It is decoration
only, so no text and no control state depends on it.

The page is complete with JavaScript off. The script on the main page adds the year and starts the handshake
animation when the terminal scrolls into view. The script on the 404 page adds the requested path to the dial
line. The animations start only on page load or when the terminal comes into view, stop in less than 5 seconds,
and do not run under `prefers-reduced-motion: reduce`. Body text does not move.

### When a design token changes

1. Copy the four files from `src/devops_cli/design/` in devops-cli into the copied blocks of `assets/tokens.css`,
   and write the new commit in its header comment.
2. Update the copies of token values that cannot read CSS variables: `assets/favicon.svg` (color.accent and
   color.bg) and the `theme-color` meta tags in `index.html` and `404.html` (`--site-desktop`).
