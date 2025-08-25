# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Context

### The Everest Lab
**Website**: theeverestlab.com

The Everest Lab is the parent brand/company that will host multiple products and software services. It serves as an umbrella organization under which various projects and applications will be developed and launched.

**Key Components**:
- Portfolio of software products and services
- Teams section (planned)
- Founder profile section (planned)
- Central hub for all projects under the brand

### Baby Joy
**Website**: babyjoy.theeverestlab.com  
**App Store**: https://apps.apple.com/sg/app/baby-joy/id6475108933

Baby Joy is the first official product launched under The Everest Lab brand. It is a comprehensive baby tracking and parenting hub application designed to help parents monitor and record their baby's growth, milestones, and daily activities.

**Features**:
- Baby growth tracking
- Milestone monitoring
- Daily activity logging
- Parenting resources and tools

### Project Structure
- **The Everest Lab** (theeverestlab.com) - Parent brand/company website
- **Baby Joy** (babyjoy.theeverestlab.com) - First product, subdomain structure
- **Future Products** - Will follow similar subdomain pattern (product.theeverestlab.com)

### Future Plans
- Expand The Everest Lab into a full-scale software services company
- Develop and launch additional applications alongside Baby Joy
- Implement Teams section on main site to showcase company structure
- Add comprehensive Founder Profile section
- Build a cohesive ecosystem of interconnected products under The Everest Lab brand

## Technical Documentation

### Commands

#### Development
- `npm run dev` - Start development server at localhost:4321
- `npm run build` - Build production site to ./dist/
- `npm run preview` - Preview production build locally

#### Code Quality
- `npm run format` - Format code with Prettier
- `npm run lint:eslint` - Run ESLint checks

#### Astro CLI
- `npm run astro add` - Add Astro integrations
- `npm run astro check` - Check TypeScript types

### Architecture Overview

#### Component Structure
This project uses a **widget-based architecture** with layered components:

- **`src/components/widgets/`** - High-level page sections (Hero, Features, CallToAction, etc.) that accept props and slots for customization
- **`src/components/ui/`** - Reusable UI primitives (Button, Timeline, ItemGrid)
- **`src/components/common/`** - Shared utilities (Analytics, Image optimization, Metadata)
- **`src/components/blog/`** - Blog-specific components with pagination and related posts

#### Routing Pattern
- **Static pages**: Direct `.astro` files in `src/pages/`
- **Dynamic blog routes**: `src/pages/[...blog]/` with nested routing for categories/tags
- **Template variations**: `src/pages/homes/` and `src/pages/landing/` for different page types
- **Content permalinks**: Configured in `src/config.yaml` with pattern variables

#### Key Configuration
- **Site settings**: `src/config.yaml` - Controls site metadata, blog settings, analytics
- **Navigation**: `src/navigation.js` - Menu structure and links
- **Custom styles**: `src/components/CustomStyles.astro` and `src/assets/styles/tailwind.css`

#### Utility Functions
- **`src/utils/blog.ts`** - Blog content fetching, filtering, pagination
- **`src/utils/permalinks.ts`** - URL generation and routing
- **`src/utils/images.ts`** - Image optimization and processing
- **`src/utils/frontmatter.mjs`** - Markdown plugins (reading time, lazy loading)

#### Content Management
- Blog posts in `src/content/post/` using MDX format
- Content Collections API for type-safe content
- Image assets in `src/assets/images/` with automatic optimization

#### Custom Integration
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