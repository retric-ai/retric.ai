# retric.ai

Source for [retric.ai](https://retric.ai): a static site with no build step (plain HTML and CSS),
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

```
index.html          single-page site
404.html            not-found page
assets/site.css     styles (light/dark via prefers-color-scheme)
assets/favicon.svg  logo mark
CNAME               custom domain for GitHub Pages
```
