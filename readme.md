# Vanilla Layout Template

A lightweight template for building websites with Vite + SCSS without framework dependencies.

## Requirements

- Node.js 18+
- npm 9+

## Quick Start

### Create Project via GitHub

1. Click **Use this template** → **Create a new repository**
2. Clone the created repository:

```bash
git clone https://github.com/YOUR_USERNAME/your-project-name.git
cd your-project-name
```

### Create Project via degit

```bash
npx degit github:YOUR_USERNAME/vanilla-layout-template your-project-name
cd your-project-name
```

### Install and Run

```bash
npm install
npm run dev
```

The project will open in your browser at `http://localhost:3000`

## Project Structure

```
├── public/                 # Static files (fonts, images)
├── scripts/                # Automation scripts
│   ├── create-page.js
│   └── create-component.js
├── src/
│   ├── pages/              # HTML page files
│   │   ├── index.html
│   │   └── about.html
│   ├── styles/
│   │   ├── abstracts/      # Variables and mixins
│   │   │   ├── _variables.scss
│   │   │   └── _mixins.scss
│   │   ├── base/           # Base styles (reset, typography)
│   │   │   └── _reset.scss
│   │   ├── components/     # UI components
│   │   │   └── _buttons.scss
│   │   ├── pages/          # Individual page styles
│   │   │   ├── home.scss
│   │   │   └── about.scss
│   │   └── main.scss       # Styles entry point
│   ├── main.js             # Script for home page
│   └── about.js            # Script for "About" page
├── dist/                   # Project build (generated automatically)
├── vite.config.js          # Vite configuration
└── package.json
```

## Commands

| Command | Description |
| :--- | :--- |
| `npm run dev` | Start development server with hot reload |
| `npm run build` | Build project to `dist` folder |
| `npm run preview` | Preview production build |
| `npm run create:page <name>` | Create a new page |
| `npm run create:component <name>` | Create a new component |

## Automation

### Create a Page

```bash
npm run create:page <name>
```

Example:

```bash
npm run create:page contact
```

This will create:

- `src/pages/contact.html`
- `src/contact.js`
- `src/styles/pages/contact.scss`
- Updates `vite.config.js` (adds entry point)

### Create a Component

```bash
npm run create:component <name>
```

Example:

```bash
npm run create:component card
```

This will create:

- `src/styles/components/_card.scss`
- Updates `src/styles/main.scss` (adds import)

## Add a Page Manually

1. Create an HTML file in `src/pages/`:

```html
<!-- src/pages/contact.html -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Contact</title>
  <script type="module" src="../contact.js"></script>
</head>
<body>
  <h1>Contact</h1>
</body>
</html>
```

2. Create a JS file in the `src/` root:

```javascript
// src/contact.js
import './styles/main.scss'
import './styles/pages/contact.scss'
```

3. Add an entry point in `vite.config.js`:

```javascript
rollupOptions: {
  input: {
    main: resolve(__dirname, 'src/pages/index.html'),
    about: resolve(__dirname, 'src/pages/about.html'),
    contact: resolve(__dirname, 'src/pages/contact.html'),
  },
},
```

## Working with Styles

### Variables

File: `src/styles/abstracts/_variables.scss`

```scss
$primary-color: #3498db;
$font-main: 'Inter', system-ui, sans-serif;
$spacing-unit: 8px;
```

### Mixins

File: `src/styles/abstracts/_mixins.scss`

```scss
@mixin flex-center {
  display: flex;
  justify-content: center;
  align-items: center;
}

@mixin breakpoint($point) {
  @if $point == 'tablet' {
    @media (max-width: 768px) { @content; }
  }
}
```

### Usage

```scss
@import '../abstracts/variables';
@import '../abstracts/mixins';

.element {
  @include flex-center;
  background: $primary-color;
}
```

## Build Project

To create a production version, run:

```bash
npm run build
```

Files will be generated in the `dist` folder:

- HTML files for each page
- Optimized CSS files (separate for each page)
- Minified JS files

## Vite Configuration

Configuration is located in `vite.config.js`. Main parameters:

- `root` — source folder (`src`)
- `build.outDir` — build folder (`dist`)
- `server.port` — development server port (3000)
- `server.open` — page to auto-open

## License

MIT