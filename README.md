# Guinane.xyz

My personal website.

![Screenshot of the website](./.github/screenshots/desktop.png)

## Operational Notes

This site is written using the [Astro](https://astro.build) framework and [Vue](https://vuejs.org).
It is rendered at compile-time and served as static HTML, CSS, plus the tiniest bit of Javascript.
For more on that, see: [_Deployment_](#deployment).

### Project Structure

```bash
├─ .github/           # scripts for build & deploy
├─ public/
│  └─ assets/         # static files, images
└─ src/
   ├─ components/     # the (mostly Vue) components
   ├─ layouts/        # templates for project pages
   └─ pages/
      ├─ project/     # project pages, in markdown
      └─ index.html   # the homepage
```

### Local Development

Clone the repository, and install the dependencies:

```bash
pnpm install
```

To build the website and host it locally, run:

```bash
pnpm run dev
```

### Images

PNG images in the [`public/assets/`](./public/assets) directory will be automatically converted into
both `webp` and `avif` formats. The image conversion occurs at compile-time, and is configured by
the `convert:img` and `local:img` npm scripts (located in the [package.json](./package.json)).

### Styleguide

This project follows the [Goodbyte Styleguide](https://github.com/GoodbyteCo/Styleguide),
enforced with an [ESLint](./.eslintrc) config. Every push to the `main` branch is checked
against the styleguide, and changes that are not formatted accordingly will fail.

The project can be linted by running:

```bash
pnpm run lint
pnpm run lint -- --fix  # will try to fix any issues
```

While this works fine enough, it is recommended that you install the
[ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) and
[Textlint](https://marketplace.visualstudio.com/items?itemName=taichi.vscode-textlint)
VS Code extensions to take advantage of auto-formatting and other IDE integrations.

### Compiling the Fonts

The sites fonts are extremely subsetted, converted to `woff2`, and inlined in base64 into the
[global stylesheet](./src/components/global-style.astro). By using this (somewhat hacky)
[font loading strategy](https://www.zachleat.com/web/comprehensive-webfonts/#inline-data-uri), the
site is able to completely avoid [FOIT and FOUT](https://css-tricks.com/fout-foit-foft/).

The font is subsetted based on which characters are actually used on the site, and therefore needs
to be updated on occasion to stay in sync. This is a semi-manual process using the font utility tool
[Glyphhanger](https://github.com/zachleat/glyphhanger). Here’s how you do it:


1. [Install Glyphhanger](https://www.sarasoueidan.com/blog/glyphhanger/) if you haven’t already

2. Create a temporary directory so you have a clean surface to work on:
	
	```bash
	mkdir temp
	cd temp
	```

3. Pull the fonts from the CDN:

	```bash
	wget https://fonts.goodbyte.ca/circular.ttf
	wget https://fonts.goodbyte.ca/circular-bold.ttf
	```

4. Subset the fonts based on characters used on the site and convert to `woff2`:
	
	```bash
	glyphhanger https://guinane.xyz --subset=*.ttf --formats=woff2
	```

5. Base64 encode the minified fonts:
	
	```bash
	base64 circular.woff2 > circular.txt
	base64 circular-bold.woff2 > circular-bold.txt
	```

6. Copy the data URIs into the global font-face declarations (overwriting what’s already there).
The declarations can be found in the [global-style.astro](./src/components/global-style.astro) file.

### Deployment

All commits and merges into the `main` branch automatically trigger a build of the site. A Github
workflow script ([deploy.yml](./.github/workflows/deploy.yml)) checks out the repository and runs
`pnpm run build`. The outputted `dist/` folder (containing the statically built site) is then
pushed to the [`compiled-site`](https://github.com/qjack001/qjack001.github.io/tree/compiled-site)
branch. Unless completely necessary, avoid committing directly to the `compiled-site` branch, as
your changes will be overridden by any future deployments.

Github Pages is configured to host the branch at [guinane.xyz](https://guinane.xyz) as-is (i.e.
without treating it as a Jekyll site). This is achieved by first adding a [`CNAME`](./public/CNAME)
file to the `public/` directory, so that it is added to the root of the `dist/` folder, and
subsequently the `compiled-site` branch. Second, the `pnpm run build` script is appended with
`touch dist/.nojekyll`, creating an empty file that tells Github Pages not to run any Jekyll
post-processing.
