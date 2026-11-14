# ukqfhf — personal website

Personal portfolio website built with [Eleventy (11ty)](https://www.11ty.dev/) and deployed to [GitHub Pages](https://pages.github.com/).

**Live site:** https://ukqfhf.github.io/ukqfhf-portfolio/

## Requirements

- [Node.js 26](https://nodejs.org/) (the project's `engines.node` range is `>=26 <27`)
- npm (included with Node.js)

## Getting started

```bash
git clone https://github.com/ukqfhf/ukqfhf-portfolio.git
cd ukqfhf-portfolio
npm ci
npm start
```

`npm start` runs Eleventy's local development server with watch mode.

## Building for production

```bash
npm run build
```

Eleventy generates the static site in `_site/`. To build with the repository-name prefix used by GitHub Pages:

```bash
npm run build -- --pathprefix=ukqfhf-portfolio
```

## Project structure

```text
src/
  assets/          # Images and local fonts (copied to the output)
  pages/           # Page templates, content and entry-point CSS
  shared/          # Reusable Nunjucks layouts, UI partials and styles
.eleventy.js       # Eleventy configuration and CSS/HTML processing
.github/workflows/
  gh-pages.yml     # Pull request checks and GitHub Pages deployment
```

The site uses **Nunjucks** for templating, **PostCSS** (with `postcss-import` and `postcss-csso`) for stylesheets, and `html-minifier-terser` for generated HTML.

## CI/CD

The [GitHub Actions workflow](.github/workflows/gh-pages.yml) uses Node.js 26.

- **Pull requests targeting `main`:** install dependencies with `npm ci` and run a production build. No deployment occurs.
- **Pushes to `main`:** build the site, upload `_site/` as a Pages artifact, and deploy it to the `github-pages` environment.
- **Manual runs:** supported via `workflow_dispatch`; deployment is restricted to the `main` branch.

Deployment uses GitHub-managed Actions permissions and OIDC; no personal access token needs to be committed to the repository.

## Further reading

- [Eleventy documentation](https://www.11ty.dev/docs/)
- [GitHub Pages documentation](https://docs.github.com/en/pages)
