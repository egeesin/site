# pxl [![Build](https://github.com/egeesin/pxl/actions/workflows/node-gulp.yml/badge.svg)](https://github.com/egeesin/pxl/actions/workflows/node-gulp.yml) <img class=left src=logo.gif width=71px align=right alt="Pixelated logo with flashy written letters 'pxl'." />

> An adjustable framework-ish website theme with sensible defaults and nice looks.

<img class=center src=preview.png alt="A screenshot of the website theme previewing both light and dark theme." />

## <span style="font-weight:400">**p**retty e**x**treme **l**ist of features 'cause I ❤️ <span title="Confusing Specificity Sufferfest">CSS</span></span>

- Focused on HTML and CSS, leaving JavaScript for implementing accessibility features and non-essential tasks only
- No CSS frameworks dependency
- CSS Reset with [Sanitize.css](https://github.com/csstools/sanitize.css)
- Improved legibility with vertical rhythm and modular scale
- Mobile-first responsive design
- Auto or manual dark mode with lots of color palette options including [Solarized](https://github.com/altercation/solarized), [Gruvbox](https://github.com/morhetz/gruvbox), [One Dark UI](https://github.com/atom/one-dark-ui) and many more for each mode.
- (Almost) every element has multiple designs to serve content in multiple ways
	- Customizable and responsive navigation component
	- Container make-ups like shadow/emboss effects, border and outer border thickness, adjustable corner roundness
	- External background layers for adding blending grain/gradient effects
- [BEM](https://getbem.com/naming/)) class naming with chainable modifier and [namespace](https://csswizardry.com/2015/08/bemit-taking-the-bem-naming-convention-a-step-further/) tweaks
- Support for basic multidirectional writing mode with [logical properties](https://css-tricks.com/css-logical-properties-and-values/) (WIP)
- Builds with [Gulp](https://gulpjs.com/) task runner and plugins for optimization, feature fallbacks, PostCSS, future CSS compatibilities, live browser view
- Optional (and also experimental) tasks like renaming class selectors, removing unused selectors

## Build

### Local Installation
Tested on GNU/Linux distros and macOS.

**Dependencies:** [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git), [pnpm](https://pnpm.io/installation) (or [npm](https://www.npmjs.com/get-npm)), [gulp](https://gulpjs.com/docs/en/getting-started/quick-start)

Open a terminal emulator and execute commands below:

```sh
# Clone the repository and change directory
git clone https://github.com/egeesin/pxl && cd pxl

# Install Node modules locally.
pnpm i # or "npm i"

# Generate your first build
gulp build

# Create live server for preview of the build
gulp watch
```

### Build Artifacts from GitHub Actions
1. Go to [**Actions**](https://github.com/egeesin/pxl/actions) tab in [repository](https://github.com/egeesin/pxl) homepage.
2. Find latest successful workflow run.
3. Scroll to bottom and download build artifacts.


## Design

Initially, *pxl* is built for my own personal [website](https://egeesin.com) for blogging, portfolio and various possible content types that I was planning to post. But as I continued the development of the theme, I have become aware of different CSS methodologies and design systems to handle complexity, various types of content and configurability of overall look without comprimising unified look of the page.

### Directory Structure and Definitions
- Root directory contains information on metadata of this repository, which files to exclude, a few configurations for CSS/JavaScript linters, license and this "README" file.
- **`src`** (Source) directory contains everything this repository has it's in core.
	- Inside **`page`**, there are relevant directories containing demo HTML pages of components, objects, layouts – or in other words: atoms, molecules, organisms, templates and pages. **_include** directory is for keeping files as reusable chunks like inside of \<head>, static parts of page header and footer used and parsed by [posthtml-include](https://github.com/posthtml/posthtml-include) plugin.
	- Inside **`style`**, CSS files are placed in different directories based on [7-1 pattern](https://sass-guidelin.es/#the-7-1-pattern) that is similar to [ITCSS](https://www.xfive.co/blog/itcss-scalable-maintainable-css-architecture/) (Inverted Triangle CSS).
		- `abstract`
		- `base`
		- `class`
	- **`script`** includes scripts to make this project functional and responsive. Responsive navigation components, selecting theme modifiers and updating ARIA attributes for better accessibility markup are the examples for providing these.
	- **`icon`** includes a custom icon set that is dedicated to this repository. It's exported from Affinity Designer as multiple SVG vector files (slices) automatically to be merged as single SVG spritesheet later.
	- `11ty` directory has filter/transform scripts, configurations and templates written with Liquid template language makes it compatible to Eleventy, static site generator.
	- `img` has placeholder images for testing responsive \<picture>/srcset attributes, favicon and customizable page backgrounds.
	- `font` contains preferred default sans-serif and monospace WOFF2 fonts.
- Among the excluded files: there's a **`dist`** (Distribution) directory for keeping the generated files that are parsed from source files; **pre-dist** (Pre-Distribution) directory for the parsed source files that aren't minimized yet; **11ty-build** for keeping 11ty-compatible templates ready to use.

### CSS Methodology/Class Naming
By chronologic order, I've used BEM (Block--Element__Modifier) naming convention, ITCSS (Inverted Triangle CSS), BEMIT (BEM + ITCSS) and other transparent UI namespaces from Harry Roberts, chainable modifiers from BEM (BEVM) and Intrinsic Web Design (influenced by Jen Simmons, Heydon Pickering & Andy Bell). I've tried to shape this project around my understandings of all these designs.

#### My Interpretation and Execution Through All Methodologies
The directory and specificity hierarchy from [ITCSS](https://www.xfive.co/blog/itcss-scalable-maintainable-css-architecture/), block and element namings from [BEM](https://getbem.com/naming/), chainable modifiers from [BEVM](https://www.slideshare.net/Jyaasa/bevm-blockelementvariation-modifier)), camelCase name groups from [ABEM](https://css-tricks.com/abem-useful-adaptation-bem/) are the design choices that I completely chose to apply as it is.

Harry Roberts' namespaces (for objects, components, utilities, theme, scope, JS states, hacks) from [BEMIT](https://csswizardry.com/2015/08/bemit-taking-the-bem-naming-convention-a-step-further/) and Intrinsic Web Design are the design choices that I chose to redefine it a little or pick only the distinctive parts of it in order to make it sensible to co-exist and readible for this project.

### Typography
All inline elements including paragraph and heading texts are proportionally sized by set modular scale. Each elements has unified vertical spacings for the sake of vertical rhythm. All those units are interconnected through --typeScale… custom properties.
Preferred default fonts are [Inter](https://rsms.me/inter/) and patched version of [Iosevka](https://typeof.net/Iosevka/) as monospace font and fallback is system font stack.

### Media Breakpoints for Responsive Design
By default, *pxl* uses mobile-first responsive design approach and expand through different
screen sizes that fits different [human ergonomics](https://x.com/lukew/status/273453112902172672).
There are viewport widths for:
- wrist (smartwatches, for screens smaller than 2 inches),
- palm (smartphones, "phablets", ≥640px),
- lap (tablets on portrait mode, ≥960px),
- desk (tablets on landscape mode, laptops, desktop PCs, ≥1280px) and,
- exaggarated custom media properties like:
	- wall (desktop PCs, full HD monitors, ≥1600px)
	- mall (2K monitors, ≥1920px) and,
	- titan (ultra-wide monitors, 4K displays, ≥2400px)

### Browser Support

All web browsers that has 0.5% or higher global usage (except Opera Mini and any other deprecated browsers) are supported.
For the details, check `browserslist` section in `package.json`.

## Roadmap

- [x] Custom icon set
- [ ] Selector whitelist for PurgeCSS and rcs
- [ ] Complete documentation
- [ ] Export options for 11ty templates
- [x] CSS Grid support
- [ ] WordPress Block Theme support
- [ ] Update CSS when implementations [below](https://caniuse.com/?feats=view-transitions,css-relative-colors,css-text-box-trim,mdn-css_types_color_color-mix,css-media-range-syntax,css-cascade-layers,mdn-css_types_length_lh,mdn-css_at-rules_property,mdn-css_types_color_oklch,css-container-queries,style-scoped,jpegxl,css-has,css-text-wrap-balance) have cross-browser support:
	- Selectors 4 ([:has](https://drafts.csswg.org/selectors-4/#relational))
	- Color Module Level 5 (Awaiting for Firefox support) ([OKLCH unit](https://drafts.csswg.org/css-color-5/#relative-OKLCH), [color-mix()](https://drafts.csswg.org/css-color-5/#color-mix), [Relative Color Syntax](https://drafts.csswg.org/css-color-5/#relative-colors))
	- [@property values](https://developer.mozilla.org/en-US/docs/Web/CSS/@property#browser_compatibility)
	- Units and Values Module Level 4 ([Exponent Functions (pow() especially)](https://www.w3.org/TR/css-values-4/#exponent-funcs), [Stepped Value Functions (round())](https://www.w3.org/TR/css-values-4/#funcdef-round), [Font-relative lengths (lh)](https://www.w3.org/TR/css-values-4/#lh))
	- env() in media queries

## License
This project is under [GNU GPL 3.0](https://www.gnu.org/licenses/gpl-3.0.html) license.
