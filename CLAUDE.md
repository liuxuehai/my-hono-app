# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a full-stack template for building a React application with TypeScript and Vite, designed to run on Cloudflare Workers with Hono as the backend framework. The project combines:

- **Frontend**: React 19 with Vite for fast development
- **Backend**: Hono.js for API routes running on Cloudflare Workers
- **Deployment**: Cloudflare Workers with edge computing capabilities
- **UI Framework**: shadcn/ui with Tailwind CSS

## Architecture

The project has a dual structure:

1. **Frontend** (`src/react-app/`): React application with TypeScript
2. **Backend** (`src/worker/`): Hono.js application that runs on Cloudflare Workers

The frontend makes API calls to `/api/` routes which are handled by the Hono backend. During development, Vite proxies these requests to the Worker dev server.

## Key Files

- `src/react-app/App.tsx`: Main React component with UI and API integration
- `src/worker/index.ts`: Hono backend with API routes
- `vite.config.ts`: Vite configuration with Cloudflare plugin
- `wrangler.json`: Cloudflare Workers configuration
- `package.json`: Dependencies and scripts
- `tailwind.config.cjs`: Tailwind CSS configuration
- `postcss.config.cjs`: PostCSS configuration
- `components.json`: shadcn/ui configuration

## Common Commands

### Development
```bash
npm run dev          # Start development server
```

### Building
```bash
npm run build        # Build for production
npm run preview      # Preview production build locally
```

### Deployment
```bash
npm run deploy       # Deploy to Cloudflare Workers
```

### Testing & Quality
```bash
npm run lint         # Run ESLint
npm run check        # Type check, build, and dry-run deploy
```

### Monitoring
```bash
npx wrangler tail    # Monitor deployed Worker logs
```

### Adding shadcn/ui Components
```bash
npx shadcn@latest add button  # Add a specific component
```

## Development Workflow

1. Frontend development happens in `src/react-app/`
2. Backend API routes are defined in `src/worker/index.ts`
3. The frontend calls `/api/` routes which are handled by the Hono backend
4. Changes to either frontend or backend are automatically reflected in development
5. For deployment, both frontend and backend are bundled and deployed to Cloudflare Workers

## Key Concepts

- API routes in Hono are automatically available at `/api/` paths in the frontend
- The Cloudflare Vite plugin handles the integration between frontend and backend during development
- Static assets are served from the `dist/client` directory after build
- The project uses React 19 with modern hooks and features
- UI components are built with shadcn/ui and Tailwind CSS
- Components can be imported using the `@/` alias (e.g., `@/components/ui/button`)

## UI Framework (shadcn/ui)

This project uses shadcn/ui, which is not a component library but a collection of re-usable components that you can copy and paste into your apps.

### Key Features:
- Built with Radix UI and Tailwind CSS
- Fully accessible
- Customizable with CSS variables
- Copy-paste friendly
- No lock-in

### Component Structure:
- Components are located in `src/react-app/components/`
- UI components are in `src/react-app/components/ui/`
- Utility functions are in `src/react-app/lib/utils.ts`

### Adding New Components:
1. Use the shadcn CLI: `npx shadcn@latest add [component-name]`
2. Or manually create components in the `components/ui/` directory

### Customization:
- Customize the theme in `tailwind.config.cjs`
- Modify CSS variables in `src/react-app/index.css`
- Update component aliases in `components.json`

### Configuration Notes:
- Configuration files use `.cjs` extension because the project is configured as an ES module (`"type": "module"` in package.json)
- PostCSS configuration uses `@tailwindcss/postcss` plugin for compatibility with Tailwind CSS v4
- PostCSS and Tailwind configurations are in CommonJS format to work properly with the ES module setup