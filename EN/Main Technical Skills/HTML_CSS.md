# HTML & CSS Interview Questions

## HTML5

<details>
<summary><b>What are the key differences between HTML and HTML5?</b></summary>

HTML5 added: semantic elements (header, nav, article), new form inputs (date, email), audio/video tags, canvas, local storage, geolocation API, web workers. Simplified doctype: `<!DOCTYPE html>`. Better mobile support.
</details>

<details>
<summary><b>What is meant by web storage in HTML5?</b></summary>

Client-side storage without cookies. Two types: LocalStorage (persists until cleared, ~5MB) and SessionStorage (cleared when tab closes). Key-value pairs, strings only. Accessed via `localStorage.setItem()/getItem()`.
</details>

<details>
<summary><b>What is the difference between span and div?</b></summary>

- `div`: Block-level element, takes full width, new line before/after
- `span`: Inline element, takes only needed width, no line breaks

Use div for layout sections, span for styling text portions.
</details>

<details>
<summary><b>What's the difference between the svg and canvas elements?</b></summary>

- **SVG**: Vector graphics (XML), scalable without quality loss, each element accessible in DOM, good for icons/logos
- **Canvas**: Bitmap/raster, pixel-based, drawn via JavaScript API, good for games/animations

SVG for static graphics, canvas for dynamic rendering.
</details>

<details>
<summary><b>What is Semantic HTML?</b></summary>

Using HTML elements for their meaning, not just appearance. Examples: `<header>`, `<nav>`, `<main>`, `<article>`, `<aside>`, `<footer>`. Benefits: accessibility (screen readers), SEO, code readability.
</details>

<details>
<summary><b>How to optimize website assets?</b></summary>

Images: compress, use WebP, lazy loading, responsive images. CSS/JS: minify, bundle, tree shake. Enable gzip/brotli compression. Use CDN. Cache headers. Critical CSS inline. Defer non-critical JS.
</details>

<details>
<summary><b>Why do we use HTML5?</b></summary>

Better multimedia support (no Flash), cleaner code with semantic tags, improved forms, offline capabilities, better mobile support, backward compatible, native APIs (geolocation, drag-drop).
</details>

<details>
<summary><b>Explain new Form input types in HTML5</b></summary>

New types: `email`, `url`, `tel`, `number`, `range`, `date`, `time`, `datetime-local`, `month`, `week`, `color`, `search`. Built-in validation, mobile keyboards adapt to input type.
</details>

<details>
<summary><b>Explain HTML5 Graphics (Canvas, SVG)</b></summary>

- **Canvas**: `<canvas>` element + JavaScript API. 2D context for drawing shapes, images, text. Good for games, visualizations. No DOM access to drawn elements
- **SVG**: XML-based markup. Each shape is DOM element. Scalable, styleable with CSS. Good for icons, charts, logos
</details>

<details>
<summary><b>What is WebGL and when would you use it?</b></summary>

WebGL is a JavaScript API for rendering 2D/3D graphics using GPU through `<canvas>`.

**Characteristics:**
- Hardware acceleration (GPU)
- Shader-based rendering
- High performance for complex graphics
- Complex to implement directly

**Use cases:** 3D scenes, data visualization, games. Overkill for simple UI.

**When to use what:**
- SVG → UI graphics, icons, diagrams
- Canvas → games, animations, high-frequency updates
- WebGL → complex 3D graphics
</details>

<details>
<summary><b>Canvas vs SVG - when to use which?</b></summary>

| Criteria | Canvas | SVG |
|----------|--------|-----|
| Graphics type | Raster (pixels) | Vector |
| DOM access | No | Yes |
| Scalability | Poor | Excellent |
| Interactivity | Manual | Native (CSS, events) |
| Performance | High for many objects | Slower with thousands |

**Canvas**: games, animations, real-time graphics.
**SVG**: icons, diagrams, interactive charts.
</details>

## CSS Fundamentals

<details>
<summary><b>Could you describe the different kinds of selectors?</b></summary>

- Element: `div`
- Class: `.classname`
- ID: `#idname`
- Attribute: `[type="text"]`
- Pseudo-class: `:hover`, `:first-child`
- Pseudo-element: `::before`, `::after`
- Combinator: `div > p` (child), `div p` (descendant), `div + p` (adjacent)
</details>

<details>
<summary><b>What is the difference between a class and an ID?</b></summary>

- **Class**: Reusable, multiple elements can have same class, lower specificity
- **ID**: Unique per page, one element only, higher specificity

Use classes for styling, IDs for JavaScript targeting or anchors.
</details>

<details>
<summary><b>What are the elements of the CSS Box Model?</b></summary>

Every element is a box with: Content (actual content) → Padding (space inside border) → Border → Margin (space outside border). `box-sizing: border-box` includes padding/border in width.
</details>

<details>
<summary><b>What are the limitations of CSS?</b></summary>

No parent selector (`:has()` is new), no variables in old browsers (custom properties now exist), specificity conflicts, browser inconsistencies, no built-in logic/loops (preprocessors help), vertical centering was historically hard.
</details>

<details>
<summary><b>What is the difference between inline, inline-block, and block?</b></summary>

- **Block**: Full width, new line, respects width/height/margin
- **Inline**: Only content width, no line break, ignores width/height, horizontal margin only
- **Inline-block**: Inline flow but respects width/height/margins
</details>

<details>
<summary><b>What are the differences between adaptive design and responsive design?</b></summary>

- **Responsive**: Fluid layouts, flexible images, media queries. Adapts smoothly to any screen size
- **Adaptive**: Fixed layouts for specific breakpoints (320px, 768px, etc.). Snaps between designs

Responsive is more flexible, adaptive can be more optimized per device.
</details>

## CSS Preprocessors (Sass, Less, Stylus)

<details>
<summary><b>What is a CSS Preprocessor? What are Sass, Less, and Stylus? Why do people use them?</b></summary>

Preprocessors extend CSS with: variables, nesting, mixins, functions, imports. Compile to regular CSS. Sass (SCSS syntax popular), Less (similar, JS-based), Stylus (minimal syntax). Benefits: DRY code, maintainability, organization.
</details>

<details>
<summary><b>Why should I use SCSS instead of using CSS directly?</b></summary>

Variables for colors/sizes, nesting for cleaner code, mixins for reusable code, partials for organization, math operations, functions. Modern CSS has variables now, but SCSS still offers more features.
</details>

<details>
<summary><b>Is it possible to import only part of a Sass file? If yes, then how?</b></summary>

Use partials (files starting with `_`). Import with `@use` or `@import`. For partial import of variables/mixins only, use `@use 'file' as namespace` and access specific items: `namespace.$variable`.
</details>

<details>
<summary><b>What is nesting in SCSS?</b></summary>

Write child selectors inside parent. Mirrors HTML structure. Example:
```scss
.nav {
  ul { list-style: none; }
  li { display: inline; }
  a { color: blue; &:hover { color: red; } }
}
```
`&` refers to parent selector.
</details>

<details>
<summary><b>What is the purpose of mixins in SCSS?</b></summary>

Reusable blocks of CSS. Can accept parameters. Example:
```scss
@mixin flex-center { display: flex; justify-content: center; align-items: center; }
.container { @include flex-center; }
```
Good for vendor prefixes, common patterns.
</details>

<details>
<summary><b>Can you explain what pseudo-classes are? Give me some examples.</b></summary>

Pseudo-classes select elements in specific state. Examples: `:hover` (mouse over), `:focus` (focused), `:first-child`, `:last-child`, `:nth-child(n)`, `:not()`, `:disabled`, `:checked`, `:empty`.
</details>

## BEM

<details>
<summary><b>What is BEM?</b></summary>

Block Element Modifier - CSS naming convention. Format: `block__element--modifier`. Example: `card__title--large`. Benefits: clear structure, avoids specificity wars, self-documenting, reusable.
</details>

<details>
<summary><b>What is a block, element, modificator in BEM?</b></summary>

- **Block**: Standalone component (`menu`, `card`, `button`)
- **Element**: Part of block, no meaning alone (`menu__item`, `card__title`)
- **Modifier**: Variant or state (`button--primary`, `menu__item--active`)
</details>

## CSS Modules

<details>
<summary><b>What are CSS modules, and how do they differ from traditional CSS stylesheets?</b></summary>

CSS Modules scope styles locally to component. Class names become unique (hashed). Import styles as object: `import styles from './Button.module.css'`. No global conflicts, explicit dependencies.
</details>

<details>
<summary><b>How do you define a CSS module, and what are some best practices for structuring your CSS module files?</b></summary>

Name file with `.module.css` extension. One module per component. Use camelCase for class names. Keep related styles together. Example: `Button.module.css` next to `Button.tsx`.
</details>

<details>
<summary><b>How do CSS modules help to solve common CSS problems like global namespace pollution and style conflicts?</b></summary>

Each class name transformed to unique hash during build (e.g., `button` → `Button_button_x7f3d`). No global scope by default. Styles only apply where explicitly imported. Eliminates accidental overrides.
</details>

<details>
<summary><b>How do you integrate CSS modules into your project, and what tools can you use to facilitate this process?</b></summary>

Built into Create React App and Next.js. For custom setup: configure webpack with `css-loader` and `modules: true`. Import: `import styles from './file.module.css'`. Use: `className={styles.button}`.
</details>

## Bootstrap

<details>
<summary><b>What is Bootstrap, and how does it differ from other CSS frameworks?</b></summary>

Popular CSS framework by Twitter. Provides: grid system, pre-built components, utilities, responsive design. Differs: most widely used, extensive documentation, consistent design system. Alternatives: Tailwind (utility-first), Bulma (flexbox-based).
</details>

## Styled-components & Emotion

<details>
<summary><b>How do styled-components work?</b></summary>

CSS-in-JS library. Write CSS in JavaScript template literals. Creates React component with styles attached. Scoped by default, supports props for dynamic styles. Example:
```javascript
const Button = styled.button`background: ${props => props.primary ? 'blue' : 'gray'}`;
```
</details>

<details>
<summary><b>What are the benefits of CSS-in-JS solutions?</b></summary>

Scoped styles (no conflicts), dynamic styling based on props/state, co-located with component, dead code elimination, automatic vendor prefixes, theming support, TypeScript integration.
</details>

## Material-UI & Ant Design

<details>
<summary><b>What is your experience with Material-UI?</b></summary>

MUI is React component library implementing Material Design. Provides: pre-built components (buttons, forms, dialogs), theming system, styled-components or emotion underneath. Good for rapid development with consistent design.
</details>

<details>
<summary><b>How do you customize Material-UI themes?</b></summary>

Use `createTheme()` to customize colors, typography, spacing. Wrap app in `ThemeProvider`. Override component styles via `styleOverrides` in theme or `sx` prop. Can customize individual components or global defaults.
</details>

## CSS Animations

<details>
<summary><b>How do you create CSS animations?</b></summary>

Two ways:
1. `@keyframes` + `animation` property: Define states at percentages, apply with animation name/duration/timing
2. `transition`: Animate property changes automatically

```css
@keyframes fade { from { opacity: 0; } to { opacity: 1; } }
.element { animation: fade 1s ease-in; }
```
</details>

<details>
<summary><b>What is the difference between transitions and animations?</b></summary>

- **Transitions**: Animate between two states, triggered by state change (hover, class), simpler
- **Animations**: Multiple keyframes, can loop, play automatically, more control

Use transitions for simple hover effects, animations for complex sequences.
</details>

## Storybook

<details>
<summary><b>What is Storybook and why is it useful?</b></summary>

UI development environment for building components in isolation. Benefits: develop without running full app, document components, visual testing, showcase to designers/stakeholders, test edge cases.
</details>

<details>
<summary><b>How do you document components in Storybook?</b></summary>

Create `.stories.js` files with component variants. Use `args` for prop controls. Add JSDoc comments. Use `@storybook/addon-docs` for MDX documentation. Configure argTypes for prop documentation.
</details>

## Practical Tasks

<details>
<summary><b>Create simple visual components with pure CSS/SCSS (card component, form styling)</b></summary>

Card: container with padding, border-radius, box-shadow. Form: consistent input styles, focus states, labels, validation states. Use flexbox/grid for layout.
</details>

<details>
<summary><b>Create difficult visual components with pure CSS/SCSS</b></summary>

Examples: custom checkbox/radio, tooltips, modals, dropdown menus, tabs, accordions. Requires: pseudo-elements, positioning, transitions, possibly CSS-only state management.
</details>

<details>
<summary><b>Create project style structure and theme</b></summary>

Organize: variables (colors, spacing, fonts), mixins, base styles, components. Theme object with consistent scales. Design tokens approach. Consider dark mode from start.
</details>

## Shadow DOM

<details>
<summary><b>What is Shadow DOM?</b></summary>

Shadow DOM isolates markup and styles from the main page. It prevents conflicts - styles inside don't leak out, outside styles don't leak in. Used in Web Components. Create with `element.attachShadow({mode: 'open'})`.
</details>

## Browser Rendering

<details>
<summary><b>What is the Browser Rendering Pipeline?</b></summary>

The browser turns code into pixels in several steps:
1. **Parse** HTML → DOM tree, CSS → CSSOM
2. **Style** calculation (combine DOM + CSSOM)
3. **Layout** (calculate positions/sizes)
4. **Paint** (fill pixels)
5. **Composite** (layer management)

Layout and painting are expensive. Reducing them improves performance.
</details>

<details>
<summary><b>What is the Critical Rendering Path?</b></summary>

The sequence of steps browser takes to render first pixels. Includes: HTML parsing, CSS parsing, render tree construction, layout, paint. Optimize by: minimizing critical resources, reducing critical path length, inlining critical CSS, deferring non-critical JS.
</details>

## Core Web Vitals

<details>
<summary><b>What are Core Web Vitals?</b></summary>

Google metrics measuring user experience:
- **LCP** (Largest Contentful Paint): Loading - main content visible < 2.5s
- **INP** (Interaction to Next Paint): Interactivity - response < 200ms
- **CLS** (Cumulative Layout Shift): Visual stability - score < 0.1

They affect SEO ranking. Measure with Lighthouse, PageSpeed Insights, or Web Vitals library.
</details>

<details>
<summary><b>What are Web Vitals (LCP, FID, CLS)?</b></summary>

Web Vitals are standardized metrics to measure the quality of navigation inside a website:

- **LCP (Largest Contentful Paint)** - Measures the time it takes for the largest visible content element to be fully loaded and rendered. A good LCP is less than 2.5 seconds.
- **FID (First Input Delay)** - Measures the time it takes for the browser to respond to the user's first interaction. A good FID is less than 100 milliseconds. (Note: FID is being replaced by INP in 2024+)
- **CLS (Cumulative Layout Shift)** - Measures visual stability by calculating the sum of layout shift scores for all unexpected layout shifts during the page lifespan. A good CLS is less than 0.1.
</details>

## Accessibility

<details>
<summary><b>What is the WAI-ARIA standard?</b></summary>

WAI-ARIA (Web Accessibility Initiative - Accessible Rich Internet Applications) is a technical specification developed by W3C. Its purpose is to improve web content and application accessibility, especially for users with disabilities who rely on assistive technologies like screen readers or alternative input devices.

**Key features:**
- Roles: Define what an element is (`role="button"`, `role="navigation"`)
- States: Dynamic conditions (`aria-expanded`, `aria-checked`)
- Properties: Characteristics (`aria-label`, `aria-describedby`)

**Usage:**
```html
<button aria-expanded="false" aria-controls="menu">Menu</button>
<nav role="navigation" aria-label="Main navigation">...</nav>
```

Use ARIA only when native HTML semantics aren't sufficient.
</details>

## Modern CSS Features

<details>
<summary><b>How to use nesting with pure CSS only?</b></summary>

CSS Nesting is now natively supported in modern browsers (2023+). You can write nested selectors directly in CSS without preprocessors:

```css
.card {
  padding: 1rem;

  .title {
    font-size: 1.5rem;
  }

  &:hover {
    background: #f0f0f0;
  }

  @media (min-width: 768px) {
    padding: 2rem;
  }
}
```

**Browser support:** Chrome 112+, Firefox 117+, Safari 17.2+. For older browsers, still use preprocessors like Sass/Less.
</details>

<details>
<summary><b>What are container queries?</b></summary>

Container queries allow styles to be applied based on the container size, instead of the viewport size. This makes components more responsive and reusable.

```css
.card-container {
  container-type: inline-size;
  container-name: card;
}

@container card (min-width: 400px) {
  .card {
    display: flex;
    flex-direction: row;
  }
}
```

**Benefits:**
- Components adapt to their container, not just viewport
- More modular and reusable components
- Better component-based design
- No JavaScript needed for responsive components
</details>

<details>
<summary><b>How does CSS Grid subgrid work?</b></summary>

CSS Grid subgrid allows a nested grid to inherit its parent grid's rows or columns. This is useful for aligning content of nested grid items with the parent grid's structure.

```css
.parent {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr;
  gap: 1rem;
}

.child {
  display: grid;
  grid-column: span 3;
  grid-template-columns: subgrid; /* Inherits parent's columns */
}
```

**Benefits:**
- Align nested content with parent grid
- No need to duplicate row/column definitions
- Cleaner markup without complex positioning
- Perfect for card layouts, forms, and data grids
</details>

<details>
<summary><b>Why does Facebook no longer want to follow the same direction as CSS-in-JS?</b></summary>

CSS-in-JS libraries (like styled-components, Emotion) don't generate static CSS files at build time. Instead, they generate JavaScript that sets styles through the CSSStyleSheet API at runtime.

**Problems identified:**
- Runtime overhead: JS must execute to apply styles
- Larger bundle sizes
- Hydration issues in SSR
- Memory consumption

**Solution:** Facebook created **StyleX** - a library that extracts styles at build time into static CSS files, getting the benefits of CSS-in-JS DX (colocation, type safety) while outputting optimized static CSS.
</details>

<details>
<summary><b>What is the proposal of the StyleX library?</b></summary>

StyleX is Facebook/Meta's CSS library that manages styles in an efficient and modular way.

**Key features:**
- **Build-time extraction**: Styles compiled to atomic CSS at build time
- **Type-safe**: Full TypeScript support
- **Deterministic**: Styles always resolve the same way
- **Small output**: De-duplicates styles, only ships what's used
- **No runtime cost**: Unlike styled-components, no JS runtime for styling

```javascript
import * as stylex from '@stylexjs/stylex';

const styles = stylex.create({
  button: {
    backgroundColor: 'blue',
    padding: '8px 16px',
  }
});

<button {...stylex.props(styles.button)}>Click</button>
```
</details>

## Advanced CSS Techniques

<details>
<summary><b>How to design a responsive grid without using any CSS frameworks?</b></summary>

**Modern CSS Grid approach:**

```css
/* Auto-responsive grid - items automatically adjust */
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1rem;
}

/* Classic 12-column grid system */
.container {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: 20px;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

.col-6 { grid-column: span 6; }
.col-4 { grid-column: span 4; }
.col-3 { grid-column: span 3; }

/* Responsive with media queries */
@media (max-width: 768px) {
  .col-6, .col-4, .col-3 {
    grid-column: span 12;
  }
}

/* Flexbox alternative */
.flex-grid {
  display: flex;
  flex-wrap: wrap;
  margin: -10px; /* Compensate for item margins */
}

.flex-item {
  flex: 1 1 calc(33.333% - 20px);
  margin: 10px;
  min-width: 250px; /* Prevents too narrow items */
}
```

**Key techniques:**
- `minmax()` for flexible but constrained sizing
- `auto-fit`/`auto-fill` for automatic column count
- `clamp()` for responsive values: `clamp(300px, 50%, 600px)`
- CSS custom properties for consistent spacing
</details>

<details>
<summary><b>Explain CSS containment and how it boosts performance</b></summary>

**CSS `contain` property** tells browser an element is independent from the rest of the page, enabling rendering optimizations.

```css
.card {
  contain: layout style paint;
  /* Or use shorthand: */
  contain: content; /* = layout + style + paint */
  contain: strict;  /* = size + layout + style + paint */
}
```

**Containment types:**

| Value | Description | Use case |
|-------|-------------|----------|
| `layout` | Element's layout is independent | Cards, list items |
| `paint` | Nothing outside element is painted inside | Widgets, modals |
| `style` | Counter/quotes don't affect outside | Isolated components |
| `size` | Element size doesn't depend on children | Fixed-size containers |
| `content` | All except size | Most components |
| `strict` | All containment | Complete isolation |

**Performance benefits:**
1. **Skips recalculation**: Browser knows changes don't affect rest of page
2. **Limits repaints**: Only contained element is repainted
3. **Enables layer optimization**: Can be promoted to own compositing layer

**Best practices:**
```css
/* Good for virtualized lists */
.list-item {
  contain: content;
  content-visibility: auto; /* Only render when in viewport */
}

/* Off-screen elements */
.hidden-panel {
  content-visibility: hidden;
}
```
</details>

<details>
<summary><b>How to build fully accessible components (WCAG standards)?</b></summary>

**Key WCAG 2.1 principles (POUR):**

1. **Perceivable:**
```html
<!-- Alt text for images -->
<img src="chart.png" alt="Sales increased 25% in Q4 2024">

<!-- Captions for media -->
<video>
  <track kind="captions" src="captions.vtt" srclang="en">
</video>

<!-- Sufficient color contrast (4.5:1 for normal text) -->
```

2. **Operable:**
```html
<!-- Keyboard accessible -->
<button onclick="submit()">Submit</button> <!-- ✓ -->
<div onclick="submit()">Submit</div> <!-- ✗ Not focusable -->

<!-- Skip links -->
<a href="#main-content" class="skip-link">Skip to main content</a>

<!-- Focus visible -->
<style>
button:focus-visible { outline: 2px solid blue; }
</style>
```

3. **Understandable:**
```html
<!-- Language declaration -->
<html lang="en">

<!-- Form labels -->
<label for="email">Email address</label>
<input id="email" type="email" aria-describedby="email-hint">
<span id="email-hint">We'll never share your email</span>

<!-- Error messages -->
<input aria-invalid="true" aria-errormessage="email-error">
<span id="email-error" role="alert">Please enter a valid email</span>
```

4. **Robust:**
```html
<!-- Semantic HTML -->
<nav aria-label="Main navigation">
  <ul role="menubar">
    <li role="none"><a role="menuitem" href="/">Home</a></li>
  </ul>
</nav>

<!-- ARIA for custom components -->
<div role="tablist">
  <button role="tab" aria-selected="true" aria-controls="panel1">Tab 1</button>
</div>
<div role="tabpanel" id="panel1">Content</div>
```

**Testing:** Use Axe, Lighthouse, NVDA/VoiceOver for screen reader testing.
</details>

<details>
<summary><b>Implement a modal system with focus trapping</b></summary>

```javascript
function Modal({ isOpen, onClose, children }) {
  const modalRef = useRef(null);
  const previousActiveElement = useRef(null);

  useEffect(() => {
    if (isOpen) {
      // Store currently focused element
      previousActiveElement.current = document.activeElement;

      // Focus first focusable element in modal
      const focusableElements = getFocusableElements(modalRef.current);
      focusableElements[0]?.focus();

      // Prevent body scroll
      document.body.style.overflow = 'hidden';
    }

    return () => {
      // Restore focus and scroll
      previousActiveElement.current?.focus();
      document.body.style.overflow = '';
    };
  }, [isOpen]);

  // Focus trap
  const handleKeyDown = (e) => {
    if (e.key === 'Escape') {
      onClose();
      return;
    }

    if (e.key !== 'Tab') return;

    const focusableElements = getFocusableElements(modalRef.current);
    const firstElement = focusableElements[0];
    const lastElement = focusableElements[focusableElements.length - 1];

    // Shift+Tab on first element -> focus last
    if (e.shiftKey && document.activeElement === firstElement) {
      e.preventDefault();
      lastElement.focus();
    }
    // Tab on last element -> focus first
    else if (!e.shiftKey && document.activeElement === lastElement) {
      e.preventDefault();
      firstElement.focus();
    }
  };

  if (!isOpen) return null;

  return createPortal(
    <div
      className="modal-overlay"
      onClick={(e) => e.target === e.currentTarget && onClose()}
      onKeyDown={handleKeyDown}
    >
      <div
        ref={modalRef}
        role="dialog"
        aria-modal="true"
        aria-labelledby="modal-title"
        className="modal-content"
      >
        {children}
        <button onClick={onClose} aria-label="Close modal">×</button>
      </div>
    </div>,
    document.body
  );
}

function getFocusableElements(container) {
  return container.querySelectorAll(
    'button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])'
  );
}
```

```css
.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal-content {
  background: white;
  padding: 2rem;
  border-radius: 8px;
  max-width: 500px;
  max-height: 90vh;
  overflow-y: auto;
}
```
</details>

<details>
<summary><b>How to fix layout shift issues in an image-heavy UI?</b></summary>

**Common causes and solutions:**

1. **Reserve space for images:**
```css
/* Aspect ratio box */
.image-container {
  aspect-ratio: 16 / 9;
  background: #f0f0f0; /* Placeholder color */
}

/* Or explicit dimensions */
<img width="800" height="600" src="image.jpg" alt="">
```

2. **Use modern CSS:**
```css
img {
  max-width: 100%;
  height: auto;
  /* Prevent layout shift during load */
  aspect-ratio: attr(width) / attr(height);
}
```

3. **Skeleton loaders:**
```css
.skeleton {
  background: linear-gradient(90deg, #f0f0f0 25%, #e0e0e0 50%, #f0f0f0 75%);
  background-size: 200% 100%;
  animation: shimmer 1.5s infinite;
}

@keyframes shimmer {
  0% { background-position: 200% 0; }
  100% { background-position: -200% 0; }
}
```

4. **Font loading optimization:**
```css
/* Prevent FOUT (Flash of Unstyled Text) */
@font-face {
  font-family: 'MyFont';
  src: url('font.woff2') format('woff2');
  font-display: swap; /* or optional/fallback */
  size-adjust: 100%; /* Match fallback metrics */
}

/* Adjust fallback font to match */
body {
  font-family: 'MyFont', system-ui;
}
```

5. **Ads and embeds:**
```css
/* Reserve space for dynamic content */
.ad-container {
  min-height: 250px;
  contain: layout;
}
```

6. **Monitor with CLS metric:**
```javascript
// Use web-vitals library
import { getCLS } from 'web-vitals';
getCLS(console.log); // Track layout shifts
```
</details>

## Performance Optimization

<details>
<summary><b>Explain TBT, LCP, CLS and how to improve each</b></summary>

**TBT (Total Blocking Time):**
Time between FCP and TTI where main thread is blocked for >50ms.

*Improvements:*
- Break up long JavaScript tasks
- Defer non-critical scripts
- Use web workers for heavy computation
- Reduce third-party script impact
- Code split and lazy load

**LCP (Largest Contentful Paint):**
Time until largest visible element renders (target: <2.5s).

*Improvements:*
```html
<!-- Preload critical resources -->
<link rel="preload" as="image" href="hero.jpg">
<link rel="preload" as="font" href="font.woff2" crossorigin>

<!-- Optimize images -->
<img
  src="hero.jpg"
  srcset="hero-480.jpg 480w, hero-800.jpg 800w"
  sizes="(max-width: 600px) 480px, 800px"
  loading="eager" <!-- Don't lazy load LCP image -->
  fetchpriority="high"
>
```
- Use CDN for assets
- Optimize server response time (TTFB)
- Remove render-blocking resources

**CLS (Cumulative Layout Shift):**
Sum of unexpected layout shifts (target: <0.1).

*Improvements:*
- Set explicit dimensions on media
- Reserve space for ads/embeds
- Avoid inserting content above existing content
- Use `transform` for animations (doesn't cause layout)
- Use `content-visibility` for off-screen content
```css
img, video { aspect-ratio: 16/9; }
.dynamic-content { min-height: 200px; }
```
</details>

<details>
<summary><b>How to apply code splitting, tree-shaking & deferred loading in SPAs?</b></summary>

**Code Splitting:**
```javascript
// Route-based splitting with React.lazy
const Dashboard = lazy(() => import('./Dashboard'));
const Settings = lazy(() => import('./Settings'));

// Component-based splitting
const HeavyChart = lazy(() => import('./HeavyChart'));

// Webpack magic comments for named chunks
const AdminPanel = lazy(() =>
  import(/* webpackChunkName: "admin" */ './AdminPanel')
);
```

**Tree-Shaking:**
```javascript
// ✓ Tree-shakable (named exports)
import { debounce } from 'lodash-es';

// ✗ Not tree-shakable (default/namespace import)
import _ from 'lodash';

// Configure in bundler
// webpack.config.js
module.exports = {
  mode: 'production', // Enables tree-shaking
  optimization: {
    usedExports: true,
    sideEffects: true
  }
};

// package.json - mark side-effect-free
{
  "sideEffects": false,
  // Or specify files with side effects
  "sideEffects": ["*.css", "./src/polyfills.js"]
}
```

**Deferred Loading:**
```html
<!-- Defer non-critical scripts -->
<script src="analytics.js" defer></script>
<script src="chat-widget.js" async></script>

<!-- Preload critical, prefetch future -->
<link rel="preload" href="critical.js" as="script">
<link rel="prefetch" href="next-page.js">
```

```javascript
// Dynamic imports for features
button.addEventListener('click', async () => {
  const { openModal } = await import('./modal');
  openModal();
});

// Intersection Observer for lazy components
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      import('./heavy-component').then(module => {
        module.init(entry.target);
      });
      observer.unobserve(entry.target);
    }
  });
});
```
</details>

## DOM & Browser APIs

<details>
<summary><b>What's the difference between innerHTML and textContent?</b></summary>

- `innerHTML`: Parses HTML, can execute scripts. Use for adding HTML structure. Security risk with user input (XSS)
- `textContent`: Plain text only, faster, no parsing. Safer for user content. Includes hidden text

Use `textContent` for text, `innerHTML` only for trusted HTML.
</details>

<details>
<summary><b>How does event delegation work?</b></summary>

Attach one event listener to parent instead of many to children. Events bubble up from target. Check `event.target` to identify clicked element:
```javascript
list.addEventListener('click', (e) => {
  if (e.target.matches('li')) handleItemClick(e.target);
});
```
Benefits: fewer listeners, works with dynamic elements.
</details>

<details>
<summary><b>What's the difference between event bubbling and capturing?</b></summary>

- **Capturing**: Event travels from root to target (top-down). Rarely used
- **Bubbling**: Event travels from target to root (bottom-up). Default behavior

```javascript
// Use capturing phase
element.addEventListener('click', handler, true);
// or { capture: true }
```
</details>

<details>
<summary><b>What's the difference between preventDefault and stopPropagation?</b></summary>

- `preventDefault()`: Stops default browser action (form submit, link navigation). Event still bubbles
- `stopPropagation()`: Stops event from bubbling up. Default action still happens

Use both when needed: `e.preventDefault(); e.stopPropagation();`
</details>

<details>
<summary><b>What is the Intersection Observer API?</b></summary>

Async way to observe element visibility in viewport or ancestor. Better than scroll listeners for: lazy loading images, infinite scroll, tracking visibility:
```javascript
const observer = new IntersectionObserver(entries => {
  entries.forEach(entry => {
    if (entry.isIntersecting) loadContent(entry.target);
  });
}, { threshold: 0.5 });
observer.observe(element);
```
</details>

<details>
<summary><b>How does requestAnimationFrame work?</b></summary>

Schedules callback before next browser repaint (~60fps). Better than `setInterval` for animations:
```javascript
function animate() {
  updatePosition();
  requestAnimationFrame(animate);
}
requestAnimationFrame(animate);
```
Pauses when tab inactive, syncs with display refresh rate.
</details>

<details>
<summary><b>What is CORS and how do you handle it?</b></summary>

Cross-Origin Resource Sharing - browser security restricting requests to different domains. Server must send CORS headers:
```
Access-Control-Allow-Origin: https://example.com
Access-Control-Allow-Methods: GET, POST
```
Handling: server-side proxy, CORS headers on API, JSONP (legacy).
</details>

<details>
<summary><b>What is reflow vs repaint?</b></summary>

- **Reflow**: Browser recalculates layout (positions, sizes). Expensive. Triggered by: dimension changes, DOM structure changes, window resize
- **Repaint**: Redraw visible elements without layout change. Cheaper. Triggered by: color, visibility, background changes

Minimize reflows: batch DOM reads/writes, use `transform` for animations.
</details>

<details>
<summary><b>How does the History API work?</b></summary>

Manipulate browser history without page reload:
```javascript
history.pushState({ page: 1 }, '', '/page-1'); // Add entry
history.replaceState({}, '', '/new-url'); // Replace current
history.back(); // Go back
window.onpopstate = (e) => handleNavigation(e.state);
```
Used by SPA routers for navigation.
</details>

<details>
<summary><b>What are polyfills and when do you need them?</b></summary>

Code that implements modern features in older browsers. Examples: Promise, fetch, Array.includes. Use when:
- Supporting older browsers (IE11)
- Using new APIs not yet widely supported

Tools: core-js, polyfill.io. Modern apps often skip for smaller bundles.
</details>
