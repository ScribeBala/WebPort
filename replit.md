# AI Image-to-Video Generator

## Overview

An AI-powered web application that transforms static images into dynamic videos using machine learning. Users can upload images and configure generation parameters (duration, motion intensity, camera movement) to create animated videos. The application provides a modern, creative-focused interface inspired by platforms like Replicate and RunwayML, with real-time generation status tracking and a history of previously generated videos.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Framework**: React with TypeScript, using Vite as the build tool and development server.

**Routing**: Wouter for lightweight client-side routing, with a single-page application structure centered around the Home page.

**UI Component System**: Radix UI primitives wrapped with custom styling via shadcn/ui. The design system uses:
- Tailwind CSS for utility-first styling with custom theme variables
- CSS variables for theming (light/dark mode support)
- Custom fonts: Inter for UI elements and Space Grotesk for headers
- Consistent spacing primitives (2, 4, 8, 12, 16, 24px units)
- Component-level hover and elevation effects

**Design Philosophy**: 
- Output-first approach where generated videos are the hero content
- Progressive disclosure with advanced controls hidden by default
- Visual breathing room with generous spacing around media
- Reference-based design drawing from modern AI creative platforms

**State Management**: 
- TanStack Query (React Query) for server state management and caching
- Local component state for UI interactions
- Query client configured with infinite stale time and no automatic refetching

**Key UI Components**:
- UploadZone: Drag-and-drop image upload with preview
- ParametersPanel: Collapsible advanced settings (duration, motion, camera movement)
- GenerationStatus: Real-time progress indicator
- VideoPlayer: Playback with download/share controls
- History: Grid display of past generations

### Backend Architecture

**Framework**: Express.js with TypeScript, running on Node.js.

**Server Configuration**:
- Express middleware for JSON parsing with raw body capture
- Request logging with timing for API routes
- Vite integration for development with HMR support
- Custom error handling and response formatting

**File Upload**: Multer middleware for multipart/form-data handling with:
- In-memory storage
- 10MB file size limit
- MIME type validation (PNG, JPG, WEBP only)

**API Design**:
- RESTful endpoints under `/api` prefix
- File upload endpoint: `POST /api/generate`
- CRUD operations for video generations
- Validation using Zod schemas from shared types

**Build Process**: 
- Client: Vite bundles React app to `dist/public`
- Server: esbuild bundles Express server to `dist/index.js`
- Separate development and production modes

### Data Storage Solutions

**Database**: PostgreSQL via Drizzle ORM with Neon serverless driver.

**Schema Design**:
- `users` table: Basic user authentication (username, password)
- `video_generations` table: Stores generation metadata including:
  - Image and video URLs
  - Status tracking (pending, processing, complete)
  - Generation parameters (duration, motion intensity, camera movement)
  - Timestamps

**Development Fallback**: In-memory storage implementation (`MemStorage`) using Maps for development/testing without database.

**Schema Validation**: Drizzle-zod for runtime validation of insert operations, ensuring type safety between database and application layers.

**Migrations**: Drizzle Kit manages schema migrations with PostgreSQL dialect, outputs to `./migrations` directory.

### External Dependencies

**AI Video Generation**: 
- Replicate API for image-to-video transformation
- Requires `REPLICATE_API_TOKEN` environment variable
- Converts uploaded images to base64 data URIs for API requests

**Database Service**:
- Neon serverless PostgreSQL
- Requires `DATABASE_URL` environment variable
- Connection pooling via `@neondatabase/serverless`

**Font Services**: 
- Google Fonts CDN for Inter and Space Grotesk typefaces
- Preconnect optimization for faster font loading

**Development Tools**:
- Replit-specific plugins for runtime error overlay, cartographer, and dev banner
- Only active in development mode with `REPL_ID` environment variable

**Third-Party UI Libraries**:
- Radix UI for accessible component primitives
- Lucide React for icons
- React Icons for social media icons
- date-fns for date formatting
- cmdk for command palette functionality
- class-variance-authority and clsx for conditional styling

**Session Management**: 
- connect-pg-simple for PostgreSQL-backed sessions (configured but not actively used in current implementation)

**Type Safety**:
- Shared schema definitions between client and server via `@shared` path alias
- Zod for runtime validation
- TypeScript strict mode enabled across the codebase