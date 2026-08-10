---
name: v0-design-guidelines
description: Apply v0-style design, shadcn/ui, Tailwind, typography, color, layout, imagery, accessibility, data-persistence/security, and modern React rules when building interfaces.
---

# Compatibility Override

This skill is adapted from the v0 system prompt for use in general agent environments. Do NOT assume any v0-specific tooling or preinstalled setup:

- Do not assume shadcn/ui, `components/ui/*`, `components.json`, or the `new-york` style is already installed. If shadcn/ui is absent, initialize it with the `new-york` style before using shadcn/ui components. If an individual component is absent, install it with the shadcn CLI before importing it.
- Do not assume Next.js. Detect the framework from the project (lockfile, config files, existing imports) and follow the framework-conditional sections below accordingly. Only when starting a brand-new project with no stated preference, default to Next.js App Router.
- There is no `GenerateImage` tool. When the design needs an image the project does not have: use a real asset the user provided if one exists; otherwise use a clearly-marked placeholder (e.g. `https://placehold.co/{w}x{h}`) with descriptive alt text and a `// TODO: replace placeholder image` comment. Never invent hotlinked third-party images.
- There is no `GenerateDesignInspiration` tool. Before any substantive design work, write a short design brief yourself (in your response or a scratch note) covering: mood/aesthetic direction, the 3-5 color palette with hex values, the 1-2 font families, and the layout concept. Then implement against that brief for consistency.

### Image and Assets

When a user provides an image or other asset (file path, pasted file, or URL) and asks you to use it:

- Copy/save it into the project under a local path (e.g. `public/images/logo.png`)
- Reference it in code (`src=`, CSS `url()`, etc.) by the local path (e.g. `/images/logo.png`), not the original external URL, unless the user explicitly asks otherwise
- Add alt text for all images, unless decorative or repetitive for screen readers

# Coding Guidelines

- When using Next.js, default to the App Router. When the project uses another framework (Vite, Remix, Astro, etc.), follow that framework's conventions instead — do not port Next.js idioms across.
- Set crossOrigin to "anonymous" for `new Image()` when rendering images on <canvas> to avoid CORS issues.
- When the JSX content contains characters like < > { } `, you always put them in a string to escape them properly:
- DON'T write: <div>1 + 1 < 3</div>
- DO write: <div>{'1 + 1 < 3'}</div>
- When JSX text content contains apostrophes or single quotes (e.g. contractions like "don't", "we'd", "it's"), always escape them using `'` or wrap in a JSX expression:
- DON'T write: <p>We'd love to help</p>
- DO write: <p>We'd love to help</p>
- OR write: <p>{"We'd love to help"}</p>
- You always implement the best practices with regards to performance, security, and accessibility.
- Use semantic HTML elements when appropriate, like `main` and `header`.
- Make sure to use the correct ARIA roles and attributes.
- Remember to use the "sr-only" Tailwind class for screen reader only text.
- Split code up into multiple components. Do not have one large page/entry file, but rather have multiple components that the page imports.
- Use SWR for data fetching, caching, and storing client-side state that needs to sync between components.
- Do NOT fetch inside useEffect. Either pass the data down from a server component (when the framework supports it) or use a library like SWR.
- Keep page metadata (title, description, theme-color, viewport) up to date with the user's request for optimal SEO — via `layout.tsx` metadata in Next.js, or the framework's equivalent (`index.html` head, react-helmet-style APIs, etc.).
- When the task involves geographic maps or complex spatial data, ALWAYS use an established library (e.g. react-simple-maps for choropleth/geographic maps, Leaflet or Mapbox for interactive maps) instead of generating raw SVG paths or coordinates by hand. Hand-rolling geographic data wastes time, produces inaccurate results, and risks timeouts.
- With regards to media within code:
- You can use `glb`, `gltf`, and `mp3` files for 3D models and audio. You use the native <audio> element and JavaScript for audio files.

## Data Persistence and Security

- Default to building real apps with proper backend storage instead of localStorage or client-side-only storage.
- NEVER use localStorage for data persistence unless explicitly requested by the user.
- When the app requires data persistence, use a real database (Postgres/Supabase/Neon/etc. — prefer whatever the project already has connected).
- NEVER implement mock authentication or client-side-only auth patterns.
- Authentication and security best practices, always:
- Password hashing with **argon2id** (e.g. the `argon2` package with `type: argon2.argon2id`, or `@node-rs/argon2`). Do not use bcrypt or unsalted hashes for new code; only keep bcrypt where an existing codebase already uses it and migration is out of scope.
- Secure session management with HTTP-only, Secure, SameSite cookies — never store session tokens in localStorage.
- Row Level Security (RLS) when using Supabase.
- Parameterized queries everywhere — never interpolate user input into SQL strings.
- Input validation and sanitization on the server, not just the client.
- Do NOT introduce an ORM to connect to a SQL database unless the user asks or the project already uses one.
- Use Redis-style stores (Upstash, etc.) only for caching, rate limiting, queues, sessions, or other ephemeral state — never as the primary database for general app data.

## Debugging

- When debugging issues, use `console.log("[debug] ...")` statements with a consistent prefix to trace execution flow, inspect variables, and identify issues.
- Use descriptive messages that clearly indicate what you're checking or what state you're examining.
- Remove the debug statements once the issue is resolved or the user has clearly moved on from that topic.

Examples:

- `console.log("[debug] User data received:", userData)`
- `console.log("[debug] API call starting with params:", params)`
- `console.log("[debug] Error occurred in function:", error.message)`

Best practices:

- Include relevant context in your debug messages
- Log both successful operations and error conditions
- Include variable values and object states when relevant

## React 19.2+

These apply to any React project on 19.2 or newer, regardless of framework:

- `useEffectEvent`: extract non-reactive logic from Effects into reusable Effect Event functions:

```tsx
import { useEffectEvent } from 'react';
function ChatRoom({ roomId, theme }) {
const onConnected = useEffectEvent(() => {
showNotification('Connected!', theme);
});
useEffect(() => {
const connection = createChatConnection(roomId);
connection.on('connected', () => {
onConnected();
});
// ...
}, [roomId]);
}
```

- `<Activity>` lets you hide and restore the UI and internal state of its children:

```tsx
import { Activity } from 'react';
<Activity mode={isShowingSidebar ? "visible" : "hidden"}>
<Sidebar />
</Activity>
```

## Next.js 16 (only when the project uses Next.js 16+)

Skip this section entirely for non-Next.js projects.

- `middleware.ts` is now `proxy.ts` (backwards compatible)
- Turbopack is the default bundler and is stable
- React Compiler support is stable (`reactCompiler` in next.config)
- `params`, `searchParams`, `headers()` and `cookies()` in Server Components and Route Handlers are async: they MUST be awaited.

### Improved Caching APIs

- `revalidateTag()` now requires a cacheLife profile as the second argument to enable stale-while-revalidate behavior:

```js
revalidateTag('blog-posts', 'max'); // or 'days', 'hours'
revalidateTag('products', { revalidate: 3600 }); // custom inline
```

- `updateTag()` (new, Server Actions only): read-your-writes semantics.
- `refresh()` (new, Server Actions only): refreshes uncached data only; doesn't touch the cache.

### Cache Components

Enabled via `cacheComponents: true` in next.config. The `"use cache"` directive caches pages, components, and functions with compiler-generated cache keys:

```tsx
// File level
'use cache'
export default async function Page() { /* ... */ }

// Component level
export async function MyComponent() {
'use cache'
return <></>
}

// Function level
export async function getData() {
'use cache'
const data = await fetch('/api/data')
return data
}
```

## Package Manager

The default package manager is **pnpm**, but always defer to the repository lockfile to choose the correct one.

## Adding Dependencies

When you need a new third-party package, FIRST install it with the shell and THEN write the code that imports it. Installing first prevents missing-module errors from showing up in the files you create.

**Required workflow:**

1. Figure out every new package you need for the task
2. Run one install command with the correct package manager (`pnpm add ...`, `npm install ...`, `yarn add ...`, or `bun add ...`)
3. After the install finishes, write or edit the files that import those packages

**Rules:**

- Do not write code that imports a new package before the install command has completed.
- Batch related packages into a single install command when possible.
- If a package is only referenced from config, tooling, or generated code, install it first anyway.
- Prefer writing files directly with file tools over running CLI scaffolding tools, since dedicated tools provide better observability and concurrency safety.

## shadcn/ui

- By default, build charts using Recharts components via shadcn/ui charts; only bring in custom components, such as ChartTooltip, when you need to.
- shadcn has recently introduced the following components: button-group, empty, field, input-group, item, kbd, spinner.
- If a shadcn skill is available in the environment, use it for component usage patterns, styling rules, and CLI workflows. Note some of its patterns (like `data-icon` on icons in buttons) only apply to the nova style — in new-york, buttons handle icon spacing automatically via CSS.
- Components already present in `components/ui/*` should be used directly. Only use the shadcn CLI to add components not already in the project or from third-party registries.

### Context Gathering

Use your file-search and file-read tools (Glob/Grep/Read or equivalents).

**Don't Stop at the First Match**

- When searching finds multiple files, examine ALL of them
- When you find a component, check if it's the right variant/version
- Look beyond the obvious - check parent components, related utilities, similar patterns

**Understand the Full System**

- Layout issues? Check parents, wrappers, and global styles first
- Adding features? Find existing similar implementations to follow
- State changes? Trace where state actually lives and flows
- API work? Understand existing patterns and error handling
- Styling? Check theme systems, utility classes, and component variants
- New dependencies? Check existing imports - utilities may already exist
- Types/validation? Look for existing schemas, interfaces, and validation patterns
- Testing? Understand the test setup and patterns before writing tests
- Routing/navigation? Check existing route structure and navigation patterns

**Use Parallel Tool Calls Where Possible**
If you intend to call multiple tools and there are no dependencies between the tool calls, make all of the independent tool calls in parallel. For example, when reading 3 files, run 3 tool calls in parallel. If some tool calls depend on previous calls to inform dependent values, call them sequentially instead. Never use placeholders or guess missing parameters in tool calls.

**Before Making Changes:**

- Is this the right file among multiple options?
- Does a parent/wrapper already handle this?
- Are there existing utilities/patterns I should use?
- How does this fit into the broader architecture?

**Search systematically: broad → specific → verify relationships**

# Design Guidelines

## Color System

ALWAYS use exactly 3-5 colors total.

**Required Color Structure:**

- Choose 1 primary brand color, appropriate for the requested design
- Add 2-3 neutrals (white, grays, off-whites, black variants) and 1-2 accents
- NEVER exceed 5 total colors without explicit user permission
- NEVER use purple or violet prominently, unless explicitly asked for
- If you override a components background color, you MUST override its text color to ensure proper contrast
- Be sure to override text colors if you change a background color

**Gradient Rules:**

- Avoid gradients entirely unless explicitly asked for. Use solid colors.
- If gradients are necessary:
- Use them only as subtle accents, never for primary elements
- Use analogous colors for gradient: blue→teal, purple→pink, orange→red
- NEVER mix opposing temperatures: pink→green, orange→blue, red→cyan, etc.
- Maximum 2-3 color stops, no complex gradients

## Typography

ALWAYS limit to maximum 2 font families total. More fonts create visual chaos and slow loading.

**Required Font Structure:**

- One font for headings (can use multiple weights) and one font for body text
- NEVER use more than two font families

**Typography Implementation Rules:**

- Use line-height between 1.4-1.6 for body text (use 'leading-relaxed' or 'leading-6')
- NEVER use decorative fonts for body text or fonts smaller than 14px

## Layout Structure

ALWAYS design mobile-first, then enhance for larger screens.

## Tailwind Implementation

Use these specific Tailwind patterns. Follow this hierarchy for layout decisions.

**Layout Method Priority (use in this order):**

1. Flexbox for most layouts: `flex items-center justify-between`
2. CSS Grid only for complex 2D layouts: e.g. `grid grid-cols-3 gap-4`
3. NEVER use floats or absolute positioning unless absolutely necessary

**Required Tailwind Patterns:**

- Prefer the Tailwind spacing scale instead of arbitrary values: YES `p-4`, `mx-2`, `py-6`, NO `p-[16px]`, `mx-[8px]`, `py-[24px]`.
- Prefer gap classes for spacing: `gap-4`, `gap-x-2`, `gap-y-6`
- Use semantic Tailwind classes: `items-center`, `justify-between`, `text-center`
- Use responsive prefixes: `md:grid-cols-2`, `lg:text-xl`
- Apply fonts via the `font-sans`, `font-serif` and `font-mono` classes in your code
- Use semantic design tokens when possible (bg-background, text-foreground, etc.)
- Wrap titles and other important copy in `text-balance` or `text-pretty` to ensure optimal line breaks
- NEVER mix margin/padding with gap classes on the same element
- NEVER use space-* classes for spacing

**Semantic Design Token Generation**

Define values for all applicable tokens in the globals.css file.

Note: All tokens represent colors except --radius, which is a rem size for corner rounding.

- Design tokens are a tool to help you create a cohesive design system. Use them while remaining creative and consistent.
- You may add new tokens when useful for the design brief.
- DO NOT use direct colors like text-white, bg-white, bg-black, etc. Everything must be themed via the design tokens in the Tailwind config and globals.css

**HTML Background Color**

- ALWAYS add the background color class to the `<html>` tag in the root layout (e.g. `<html className="bg-background">` in Next.js, or on the `<html>` element in `index.html` for Vite-style apps)
- If there is no root layout/entry HTML controlling `<html>`, create one and add the background color

**Fonts — Next.js projects**

Modify the root layout to add fonts via `next/font` and ensure globals.css is up to date. Use the `font-sans`, `font-mono`, and `font-serif` classes in your code for the fonts to apply:

```tsx
/* app/layout.tsx */
import { Geist, Geist_Mono } from 'next/font/google'

const geistSans = Geist({ subsets: ['latin'], variable: '--font-sans' })
const geistMono = Geist_Mono({ subsets: ['latin'], variable: '--font-mono' })

export default function RootLayout({ children }: { children: React.ReactNode }) {
return (
<html className={`bg-background ${geistSans.variable} ${geistMono.variable}`}>
<body>{children}</body>
</html>
)
}
```

```js
/* tailwind.config.js */
module.exports = {
theme: {
extend: {
fontFamily: {
sans: ['var(--font-sans)'],
mono: ['var(--font-mono)'],
},
},
},
}
```

**Fonts — non-Next.js projects**

Use `@fontsource` packages (preferred, self-hosted) or a `<link>` tag in the entry HTML, then map the families through the same CSS-variable → Tailwind `fontFamily` pattern so `font-sans`/`font-mono`/`font-serif` classes still work:

```ts
/* main.tsx (Vite) */
import '@fontsource-variable/geist'
import '@fontsource-variable/geist-mono'
```

```css
/* globals.css */
:root {
--font-sans: 'Geist Variable', sans-serif;
--font-mono: 'Geist Mono Variable', monospace;
}
```

## Visual Elements & Icons

**Visual Content Rules:**

- Use images to create engaging, memorable interfaces
- Prefer real assets the user provided. When no real asset exists, use a clearly-marked placeholder (`https://placehold.co/{w}x{h}`) with descriptive alt text and a `// TODO: replace placeholder image` comment — and tell the user which images need replacing
- NEVER generate abstract shapes like gradient circles, blurry squares, or decorative blobs as filler elements
- NEVER create SVGs directly for complex illustrations or decorative elements
- NEVER hand-draw SVG paths for geographic maps, state/country boundaries, or cartographic data. Always use a mapping library (e.g. react-simple-maps, Leaflet, or Mapbox) instead.
- NEVER use emojis as icons

**Icon Implementation:**

- Use the project's existing icon set if available (e.g. lucide-react in shadcn projects)
- Use consistent icon sizing: typically 16px, 20px, or 24px
- NEVER use emojis as replacements for proper icons

**IF the user asks for a clone or specific design**

- Follow the source as closely as possible
- Study the source website (fetch it or ask the user for screenshots) if necessary
- NEVER create anything malicious or for phishing

**Final Rule**

Ship something interesting rather than boring, but never ugly. Before any substantive design work, write a short design brief (aesthetic direction, 3-5 color palette with hex values, 1-2 font families, layout concept) and implement against it.