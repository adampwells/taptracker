# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Tap Tracker is a Quasar Framework v2 application using Vue 3 with Vite. Quasar is a Vue-based framework for building responsive applications that can target multiple platforms (SPA, SSR, PWA, Mobile, Desktop, Browser Extension).

## Common Commands

### Development
```bash
npm run dev
# or
quasar dev
```
Starts development server with hot-code reloading and error reporting. Browser opens automatically.

### Build
```bash
npm run build
# or
quasar build
```
Builds the application for production. Output goes to `dist/` directory.

### Linting
```bash
npm run lint
# or
yarn lint
```
Runs ESLint with flat config. Always run after making code changes to catch issues.

### Install Dependencies
```bash
yarn
# or
npm install
```
Run `npm run postinstall` or `quasar prepare` if needed after dependency changes.

## Architecture

### Framework Configuration
- **quasar.config.js**: Main configuration file for Quasar CLI, build settings, dev server, and platform-specific options
- Configured for hash routing mode (`vueRouterMode: 'hash'`)
- Public path set to `/taptracker/`
- Supports SSR, PWA, Cordova, Capacitor, Electron, and Browser Extension modes (configured but not necessarily all active)
- ESLint integration via vite-plugin-checker during builds

### Directory Structure
```
src/
├── App.vue              # Root component
├── layouts/             # Page layouts (MainLayout.vue provides drawer navigation)
│   └── MainLayout.vue
├── pages/               # Route-level page components
│   ├── IndexPage.vue
│   └── ErrorNotFound.vue
├── components/          # Reusable components (EssentialLink.vue)
├── router/              # Vue Router configuration
│   ├── index.js        # Router instance creation
│   └── routes.js       # Route definitions
├── boot/                # Boot files for app initialization (currently empty)
├── css/                 # Global styles
│   ├── app.scss        # Global application styles
│   └── quasar.variables.scss  # Quasar theme variables
└── assets/              # Static assets
```

### Routing
- Uses Vue Router with hash history by default
- Routes defined in `src/router/routes.js`
- Router instance uses `defineRouter` wrapper from Quasar
- Layout-based routing pattern: MainLayout wraps child routes
- 404 catch-all route included

### Component Imports
- Quasar components auto-imported (no need to manually import/register)
- Layout and page components use lazy loading: `() => import('path/to/component.vue')`
- Non-route components imported directly

### Styling
- Uses SCSS
- Quasar theme variables in `src/css/quasar.variables.scss`
- Global styles in `src/css/app.scss`
- Quasar extras: Roboto font and Material Icons included

### ESLint Configuration
- Uses flat config format (eslint.config.js)
- Vue essential rules enabled
- Browser and Node globals available
- Custom rules: allows debugger in development, disables prefer-promise-reject-errors
