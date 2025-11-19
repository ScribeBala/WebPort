# AI Image-to-Video Generator - Design Guidelines

## Design Approach

**Selected Approach:** Reference-Based with Creative Tool Inspiration

Drawing from modern AI creative platforms (Replicate, RunwayML, Midjourney) while maintaining utility-focused clarity. The design balances professional credibility with creative expression, emphasizing visual output and workflow efficiency.

**Core Principles:**
- Output-first: Generated videos are the hero content
- Progressive disclosure: Advanced controls hidden until needed
- Immediate feedback: Clear status throughout generation process
- Visual breathing room: Generous spacing around media content

---

## Typography System

**Font Stack:**
- Primary: Inter (Google Fonts) - UI, buttons, labels
- Accent: Space Grotesk (Google Fonts) - Headers, feature callouts

**Hierarchy:**
- Hero/Page Titles: Space Grotesk, 3xl-4xl weight-bold
- Section Headers: Space Grotesk, 2xl weight-semibold  
- Body Text: Inter, base-lg weight-normal
- UI Labels: Inter, sm weight-medium
- Captions/Meta: Inter, xs-sm weight-normal

---

## Layout System

**Spacing Primitives:** Tailwind units of 2, 4, 8, 12, 16, 24
- Tight spacing: 2-4 (button padding, inline elements)
- Standard spacing: 8-12 (component gaps, card padding)
- Section spacing: 16-24 (between major sections)

**Grid Structure:**
- Container: max-w-7xl with px-4 md:px-8
- Upload/Generation Area: max-w-4xl centered
- History Grid: grid-cols-1 md:grid-cols-2 lg:grid-cols-3 with gap-8

---

## Component Library

### Hero Section
- Full-width gradient background area (80vh)
- Centered content with max-w-3xl
- Large heading + descriptive subheading (max-w-2xl)
- Primary CTA: "Start Creating" + secondary "View Examples"
- Hero background: Abstract motion graphics or animated grid pattern suggesting video generation

### Upload Interface
- Prominent drag-and-drop zone (400-500px height on desktop)
- Dashed border with rounded-2xl corners
- Large upload icon (Heroicons: CloudArrowUpIcon)
- Clear "Drop image here or click to browse" instruction
- Accepted formats display: "PNG, JPG, WEBP up to 10MB"
- Preview thumbnail grid showing uploaded image with replace/remove actions

### Parameter Controls Panel
- Collapsible section below upload zone
- Clean list layout with label-input pairs
- Controls: Duration slider (1-10s), Motion intensity (Low/Med/High radio), Camera movement dropdown
- Each control with inline help icon (Heroicons: InformationCircleIcon) triggering tooltip

### Generation Status
- Fixed-width card (max-w-md) with status updates
- Progress bar with percentage
- Status messages: "Processing image...", "Generating frames...", "Rendering video..."
- Estimated time remaining
- Cancel button (subtle, secondary style)

### Video Player Card
- Generated video in 16:9 aspect ratio container
- Custom controls overlay: play/pause, timeline scrubber, volume, fullscreen
- Download button (Heroicons: ArrowDownTrayIcon) prominently placed
- Share options: Copy link, Twitter, LinkedIn icons
- Regenerate option with different parameters

### Generation History
- Three-column grid on desktop, two on tablet, one on mobile
- Each history card: Thumbnail, generation date, parameters used, quick actions (play, download, delete)
- Hover state reveals full-size preview
- "Load More" pagination at bottom

### Navigation Header
- Sticky top navigation with backdrop blur
- Logo left, navigation center (Features, Pricing, API), user account right
- Credits/usage indicator for logged-in users
- CTA button: "Upgrade" for free tier users

### Footer
- Two-column layout: Company info + Quick links | Newsletter signup
- Social media icons (Heroicons social set)
- Trust indicators: "Powered by Replicate", usage stats
- Legal links row at bottom

---

## Animations

**Minimal, purposeful motion:**
- Upload zone: Subtle pulse on drag-over state
- Generation status: Smooth progress bar animation
- Video thumbnail: Scale on hover (scale-105)
- No scroll-triggered animations
- Page transitions: Simple fade-in for new content

---

## Accessibility Standards

- All interactive elements have visible focus states with 2px offset ring
- Color contrast meets WCAG AA for all text
- Skip to main content link
- Keyboard navigation for all controls
- ARIA labels for icon-only buttons
- Video player accessible with keyboard controls
- Form inputs with visible labels (not just placeholders)
- Error states with icons + text descriptions

---

## Images

**Hero Section:**
- Large hero image showcasing example image-to-video transformation
- Split-screen comparison: Static image on left → animated video still on right
- Soft vignette overlay to ensure text readability
- Buttons over image have backdrop-blur-md background

**Feature Section:**
- Three example transformation cards
- Each showing before (static image) and after (video thumbnail with play overlay)
- Diverse examples: Portrait, Landscape, Product shot

**No custom SVG icons** - exclusively use Heroicons library via CDN for all iconography.