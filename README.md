# Glassmorphism UI Kit for Oracle APEX

Frosted glass for Oracle APEX Universal Theme: translucent panels with a thin light edge blur the colorful page behind them. One CSS file styles every Universal Theme component, in light and dark mode, without changing your pages, templates or template options.

[![Live demo](https://img.shields.io/badge/Live_demo-5468ee?style=for-the-badge)](https://oracleapex.com/ords/r/aamirkhanz/plugins/glassmorphism-ui-kit) &nbsp; Sign in as `demo` with the password `Demo`.

![Overview in light mode](screenshots/overview-light.png)

| | |
|---|---|
| **Files** | `glassmorphism.css` (the look), `glassmorphism.js` (optional light/dark switch) |
| **Version** | 1.0.3 |
| **Built for** | Oracle APEX 26.2, Universal Theme with the Iris theme style (tested); other styles are not tested yet |
| **Browsers** | Current Chrome, Edge, Safari and Firefox (the blur uses `backdrop-filter`; without it the panels stay, unblurred) |
| **License** | MIT |

## What it styles

Every component of the Universal Theme reference: Alert, Avatar, Badge, Badges List, Breadcrumb, Button, Button Container, Button Group, Calendar, Card Regions, Card Templates, Carousel, Charts, Classic Report, Collapsible, Column Toggle Report, Comments, Content Block, Content Row, Contextual Info, Flexbox Container, Form Field (every item type and label template), Help Text, Hero, Image, Inline Dialog, Interactive Grid, Interactive Report, Links List, List View, Media List, Menu Bar, Menu Popup, Metric Card, Navigation Bar, PL/SQL Dynamic Content, Reflow Report, Region Display Selector, Standard, Static Content, Tabs Container, Timeline, Title Bar and Tree.

It also styles the page shell (frosted header, side navigation and title bar over a colorful backdrop), modal and inline dialogs, drawers, popups, menus, page messages, tooltips, the date picker, Faceted Search, the rich text editor and select lists.

## Install

1. Download `glassmorphism.css` and, for the light/dark switch, `glassmorphism.js` from the [latest release](https://github.com/aamirkhanz/apex-glassmorphism-ui-kit/releases/latest) or from this repository.
2. In App Builder, go to **Shared Components > Static Application Files** and upload both files.
3. Go to **Shared Components > User Interface Attributes** and add:
   - CSS File URLs: `#APP_FILES#glassmorphism.css`
   - JavaScript File URLs: `#APP_FILES#glassmorphism.js`

That's all: every page of the application now uses the kit. Remove the two URLs to go back to plain Universal Theme.

## Dark mode

![Forms in dark mode](screenshots/forms-dark.png)

`glassmorphism.js` switches between light and dark and remembers the choice (localStorage `gm-mode`); until the user chooses, it follows the operating system.

- Add a button or link with the attribute `data-gm-mode-toggle`, or call `glassmorphism.toggle()`.
- `glassmorphism.setMode( "light" | "dark" | "auto" )` sets a mode; `glassmorphism.getMode()` returns the current one.
- `<html>` fires `gm-modechange` with `detail.mode` after a change, for example to redraw charts.

To open each page in the saved mode without a flash, put this snippet in the page template's HTML header, before the CSS:

```html
<script>(function(d){var m;try{m=localStorage.getItem("gm-mode")}catch(e){}
if(m!=="dark"&&m!=="light")m=matchMedia("(prefers-color-scheme: dark)").matches?"dark":"light";
d.documentElement.classList.add("gm-"+m)})(document);</script>
```

Without the JavaScript, the kit is light; add the class `gm-dark` to `<html>` yourself for dark.

## Make it yours

Override the tokens in your own CSS, loaded after the kit:

```css
:root { --gm-accent: #0e9f6e; --gm-accent-2: #0b7a55; --gm-blur: 24px; --gm-radius: 16px; }
:root { --gm-page: linear-gradient(135deg, #c9e4ff, #f7d6ff); }   /* your own backdrop, or a photo: url(...) center / cover */
html.gm-dark { --gm-accent: #34d399; }
```

| Token | What it sets |
|---|---|
| `--gm-page`, `--gm-page-base` | The colorful page backdrop behind the glass, and the color under it |
| `--gm-bg` | Glass of regions, cards and buttons |
| `--gm-surface-2` | The more frosted glass of popups, menus, dialogs and the chosen tab |
| `--gm-well` | Fields |
| `--gm-blur`, `--gm-saturate` | How much the glass blurs and brightens what lies behind it (default 18px, 170%) |
| `--gm-edge`, `--gm-sheen` | The thin light edge of every panel and its brighter top |
| `--gm-accent`, `--gm-accent-2` | Accent color and the end of its gradient (hot buttons, brand, selections) |
| `--gm-text`, `--gm-text-2` | Text and secondary text |
| `--gm-radius`, `--gm-radius-sm` | Corner rounding of regions, and of buttons and fields |
| `--gm-success`, `--gm-warning`, `--gm-danger`, `--gm-info` | Status colors |

For your own regions, items and HTML, add a CSS class: `gm-glass`, `gm-glass-sm`, `gm-frost` (more frosted), `gm-clear` (no glass), `gm-inset`, `gm-pill` or `gm-accent`.

## Screenshots

| | |
|---|---|
| ![Buttons](screenshots/buttons-light.png) | ![Alerts](screenshots/alerts-light.png) |
| ![Cards in dark mode](screenshots/cards-dark.png) | ![Interactive Report](screenshots/reports-light.png) |
| ![Overview in dark mode](screenshots/overview-dark.png) | ![Charts in dark mode](screenshots/charts-dark.png) |

## Notes

- **No markup changes.** The kit only overrides Universal Theme's CSS variables and adds glass to its components; your templates and template options stay standard.
- **Accessibility.** The glass is opaque enough for WCAG AA text contrast over the backdrop, fields have a visible edge, keyboard focus always shows a ring, and motion is reduced when the user asks for it.
- **Performance.** Only the outer surfaces blur (header, navigation, regions, dialogs, menus); panels inside them reuse that blur, so large pages and grids stay smooth.
- **Select lists.** In browsers with customizable selects (Chrome and Edge 135 and later) the open list takes the kit's style; other browsers show their native list.
- **Charts.** Chart series keep the colors you set in each chart; the kit styles the region around them.

## License

MIT, see [LICENSE](LICENSE).

## More

Plug-ins and updates for Oracle APEX by [TechRevX](https://www.techrevx.com). More UI kits: [Neumorphism UI Kit](https://github.com/aamirkhanz/apex-neumorphism-ui-kit), [Skeuomorphism UI Kit](https://github.com/aamirkhanz/apex-skeuomorphism-ui-kit), [Minimal Pro UI Kit](https://github.com/aamirkhanz/apex-minimal-pro-ui-kit), [Material 3 Expressive UI Kit](https://github.com/aamirkhanz/apex-material-expressive-ui-kit), [Claymorphism UI Kit](https://github.com/aamirkhanz/apex-claymorphism-ui-kit), [Liquid Glass UI Kit](https://github.com/aamirkhanz/apex-liquid-glass-ui-kit), [Swiss Grid UI Kit](https://github.com/aamirkhanz/apex-swiss-grid-ui-kit).
