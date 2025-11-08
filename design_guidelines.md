# Design Guidelines: Funnel Copywriter Dashboard

## Design Approach
**System-Based Approach**: Modern productivity dashboard following Material Design principles adapted for a professional B2B application. Focus on clarity, efficiency, and content readability with sophisticated information architecture.

## Typography System

**Font Stack**: 
- Primary: Inter (Google Fonts) - clean, professional, excellent readability
- Monospace: JetBrains Mono - for code/data display if needed

**Hierarchy**:
- Page Title: text-3xl font-bold
- Section Headers: text-xl font-semibold
- Form Labels: text-sm font-medium
- Body/Form Inputs: text-base
- Helper Text: text-sm
- Output Content H1: text-2xl font-bold
- Output Content H2: text-xl font-semibold
- Output Content H3: text-lg font-medium
- Output Body: text-base leading-relaxed

## Layout System

**Spacing Primitives**: Use Tailwind units of **4, 6, 8, 12** for consistency
- Component padding: p-6, p-8
- Section spacing: space-y-6, space-y-8
- Form field gaps: gap-6
- Container max-width: max-w-7xl

**Grid Structure**:
- Two-panel layout: Form inputs (left) | Output display (right) on desktop
- Stack vertically on mobile
- Form panel: ~40% width, sticky positioning
- Output panel: ~60% width, scrollable
- Use `lg:grid lg:grid-cols-5` with form taking `col-span-2` and output `col-span-3`

## Component Library

### Multi-Step Form
- Progress indicator at top: Step counter + percentage + visual progress bar (h-2 rounded-full)
- Step navigation clearly visible
- Field grouping with subtle dividers (border-t with py-6 spacing)
- Form container: Rounded corners (rounded-lg), padding p-8
- Fields arranged vertically with consistent gap-6 spacing

### Input Fields
**Text Inputs**:
- Rounded borders (rounded-md)
- Padding: px-4 py-3
- Border width: border-2
- Focus states: ring-2 offset pattern
- Label above input with mb-2 spacing

**Textareas**:
- Min height: min-h-32 for standard fields
- Larger for "Funnel Strategy": min-h-48
- Resize: resize-none for consistency

**Optional Field Indicator**:
- Display "(Optional)" in label with reduced opacity
- Same styling as required fields

### Buttons
**Primary CTA** (Next/Submit):
- Size: px-8 py-3
- Font: text-base font-semibold
- Rounded: rounded-lg
- Full width on mobile, auto on desktop

**Secondary** (Back):
- Ghost/outline style
- Same dimensions as primary

### Output Panels
**Three Separate Cards**:
- Equal height initially, expand with content
- Rounded: rounded-xl
- Padding: p-8
- Vertical stack on mobile, maintain order

**Empty State**:
- Document icon (from Heroicons) at 4rem size
- Placeholder text: text-lg centered
- Vertical centering: min-h-64 flex items-center justify-center

**Content Display**:
- Markdown rendered with prose classes: `prose prose-lg max-w-none`
- Custom prose styling for headings spacing
- Code blocks: rounded-md with p-4
- Lists: Proper indentation with pl-6

**Loading State**:
- Animated pulse on skeleton or spinner icon
- "Generating..." text below
- Maintain min-height during load

### Header
- Page title with icon
- Subtitle/description below (text-base opacity-80)
- Spacing: pb-8 mb-8 with border-b

### Navigation/Progress
- Sticky progress bar at top of form
- Clear step indicators (1 of 2, 50% Complete)
- Visual progress bar fills proportionally

## Streaming Content Behavior
- Content appears progressively as it streams
- Auto-scroll to latest content
- Smooth append animations (no harsh jumps)
- Final state clearly indicated

## Responsive Breakpoints
- Mobile (base): Single column, form then outputs
- Tablet (md): Consider stacking or simple 2-col
- Desktop (lg+): Side-by-side layout with form sticky

## Icons
- Use **Heroicons** (outline variant) via CDN
- Document icon for empty output states
- Checkmark for completed steps
- ChevronRight for navigation

## Accessibility
- All form inputs have associated labels
- Focus visible states on all interactive elements
- Proper heading hierarchy in outputs
- ARIA labels for progress indicators
- Keyboard navigation support throughout

## Markdown Styling
- H1-H6: Progressive size reduction with consistent spacing
- Paragraphs: mb-4 spacing
- Lists: mb-4 with proper nesting
- Bold/Italic: Preserved font-weight and style
- Code inline: rounded px-2 py-1
- Blockquotes: border-l-4 pl-4 italic

## Loading & Error States
**Loading**:
- Spinner or pulse animation
- Disable form during submission
- Show in each output panel independently

**Error**:
- Alert banner above affected section
- Retry button when applicable
- Clear error messaging

This design creates a professional, efficient workflow for users to input data and receive AI-generated content with optimal readability and minimal friction.