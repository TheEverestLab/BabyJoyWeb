# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

### Development
- `npm run dev` - Start development server at localhost:4321
- `npm run build` - Build production site to ./dist/
- `npm run preview` - Preview production build locally

### Code Quality
- `npm run format` - Format code with Prettier
- `npm run lint:eslint` - Run ESLint checks

### Astro CLI
- `npm run astro add` - Add Astro integrations
- `npm run astro check` - Check TypeScript types

## Architecture Overview

### Component Structure
This project uses a **widget-based architecture** with layered components:

- **`src/components/widgets/`** - High-level page sections (Hero, Features, CallToAction, etc.) that accept props and slots for customization
- **`src/components/ui/`** - Reusable UI primitives (Button, Timeline, ItemGrid)
- **`src/components/common/`** - Shared utilities (Analytics, Image optimization, Metadata)
- **`src/components/blog/`** - Blog-specific components with pagination and related posts

### Routing Pattern
- **Static pages**: Direct `.astro` files in `src/pages/`
- **Dynamic blog routes**: `src/pages/[...blog]/` with nested routing for categories/tags
- **Template variations**: `src/pages/homes/` and `src/pages/landing/` for different page types
- **Content permalinks**: Configured in `src/config.yaml` with pattern variables

### Key Configuration
- **Site settings**: `src/config.yaml` - Controls site metadata, blog settings, analytics
- **Navigation**: `src/navigation.js` - Menu structure and links
- **Custom styles**: `src/components/CustomStyles.astro` and `src/assets/styles/tailwind.css`

### Utility Functions
- **`src/utils/blog.ts`** - Blog content fetching, filtering, pagination
- **`src/utils/permalinks.ts`** - URL generation and routing
- **`src/utils/images.ts`** - Image optimization and processing
- **`src/utils/frontmatter.mjs`** - Markdown plugins (reading time, lazy loading)

### Content Management
- Blog posts in `src/content/post/` using MDX format
- Content Collections API for type-safe content
- Image assets in `src/assets/images/` with automatic optimization

### Custom Integration
The `vendor/integration/` directory contains custom Astro integration that:
- Virtualizes YAML config as importable modules
- Automatically updates robots.txt with sitemap
- Provides build-time optimizations

### Development Patterns
- Use existing widget components from `src/components/widgets/` when building pages
- Follow Tailwind CSS utility classes pattern
- Images should use the `<Image>` component from `src/components/common/Image.astro`
- Blog posts support both `.md` and `.mdx` with frontmatter metadata
- Path aliases: `~` maps to `src/` directory

### Performance Considerations
- Images are automatically optimized using Squoosh
- CSS/JS compression enabled in production
- Lazy loading implemented for images
- Static site generation (SSG) by default