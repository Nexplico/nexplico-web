# Agent Guide for Nexplico Web

This document outlines the standards, workflows, and conventions for AI agents (and human developers) working on the Nexplico Ltd. website. This is a static HTML5 website utilizing Tailwind CSS.

## 1. Project Overview & Architecture

- **Type:** Static Website (Single Page Application structure).
- **Core Technology:** HTML5, Tailwind CSS (CDN), Font Awesome (CDN).
- **Language:** Japanese (primary content), English (meta/code).
- **Font:** Noto Sans JP (Google Fonts).

## 2. Build, Lint, and Test Commands

Since this is a static site without a build pipeline, the "build" process is simplified.

### Build & Run
- **No Compilation:** There is no `npm build` or compilation step.
- **Local Development:**
  To preview changes, run a simple HTTP server in the root directory:
  ```bash
  # Python 3
  python3 -m http.server 8000
  
  # Node.js (if available)
  npx http-server .
  ```
- **Access:** Open `http://localhost:8000` in your browser.

### Linting & Formatting
- **Standard:** Use standard HTML/CSS formatting rules.
- **Indentation:** **4 spaces** for HTML to match existing file structure.
- **Line Length:** Soft limit of 120 characters.
- **Validation:**
  - Ensure all HTML tags are properly closed.
  - Verify Tailwind class names are correct (no typos in utility classes).
  - Check for unique IDs on sections (`#about`, `#services`, etc.).

### Testing
- **Manual Verification (Required):**
  - **Visual Check:** Open the modified page in a browser.
  - **Responsive Check:** Resize window to Mobile (xs), Tablet (md), and Desktop (lg/xl) widths.
    - *Key Checkpoint:* Ensure the navbar and grid layouts stack correctly on mobile.
  - **Navigation:** Click all navbar links to ensure smooth scrolling to the correct section.
  - **Forms:** Verify the Formspree action URL is preserved in the contact form.

## 3. Code Style Guidelines

### HTML Structure
- **Semantic Tags:** strictly use semantic elements (`<nav>`, `<header>`, `<main>`, `<section>`, `<footer>`, `<article>`).
- **Sectioning:** Each major landing page section must have an `id` matching the navbar links.
  ```html
  <section id="services" class="py-24 ...">
      <!-- Content -->
  </section>
  ```
- **Attributes:**
  - `alt`: Mandatory for all `<img>` tags.
  - `aria-label`: Use for buttons/links that contain only icons (e.g., social links).
  - `target="_blank"`: Always add `rel="noopener noreferrer"` for security.

### CSS & Tailwind
- **Usage:** Use Tailwind utility classes for 99% of styling.
- **Inline Styles:** Avoid `style="..."` attribute. Use Tailwind arbitrary values (e.g., `w-[350px]`) if standard classes don't fit, or add to the `<style>` block in `<head>` if it's a reusable pattern.
- **Class Ordering:** Organize classes logically to improve readability:
  1.  **Layout/Position:** `flex`, `grid`, `absolute`, `fixed`, `z-10`
  2.  **Spacing/Sizing:** `w-full`, `h-16`, `p-4`, `m-0`, `gap-4`
  3.  **Typography:** `text-xl`, `font-bold`, `text-center`, `text-gray-900`
  4.  **Visuals:** `bg-white`, `border`, `rounded-xl`, `shadow-sm`
  5.  **Interactivity:** `hover:bg-blue-700`, `transition`, `cursor-pointer`
  6.  **Responsive:** `md:flex`, `lg:grid-cols-3`
  
  *Example:*
  ```html
  <div class="flex items-center justify-between p-4 bg-white shadow-sm hover:shadow-md transition">
  ```

### JavaScript
- **Current State:** No custom JS files.
- **Future Additions:**
  - If adding logic (e.g., mobile menu toggle), create `assets/js/main.js`.
  - Link it at the end of the `<body>` tag.
  - Use `const`/`let` (no `var`).

### Assets
- **Images:** Place in `assets/images/`.
- **Naming:** Use kebab-case for filenames (e.g., `company-logo.png`).
- **Optimization:** Prefer WebP or optimized PNG/JPG.

## 4. Conventions & Best Practices

### Content Management
- **Japanese Text:** modifying Japanese text requires strict attention to detail. Do not introduce encoding errors.
- **Placeholders:** If adding new sections, use realistic text related to "AI", "Semiconductors", or "Embedded Systems", not "Lorem Ipsum".

### Git Commit Messages
- **Format:** `type: subject`
- **Types:**
  - `feat`: New content or section.
  - `fix`: Bug fix or typo correction.
  - `style`: Formatting or visual changes (CSS).
  - `refactor`: HTML structure improvement without visual change.
  - `docs`: Documentation updates.
- **Example:** `feat: add new team member section to about page`

### Error Handling
- **Forms:** The contact form uses Formspree. Do not modify the `action` URL or the `name` attributes (`email`, `message`, `_gotcha`) as these are required for the backend service to work.

## 5. Tool-Specific Rules

### Cursor / AI Rules
*(No specific `.cursorrules` file exists currently. Adhere to the following)*
- **Context:** When editing `index.html`, always read the surrounding 20 lines to understand the nesting level.
- **Atomic Edits:** Do not rewrite the entire file for a small change. Use search/replace or targeted edits.
- **Preservation:** carefully preserve `class` strings. Do not accidentally remove Tailwind classes when adding new ones.

### Copilot Instructions
*(No `.github/copilot-instructions.md` exists currently)*
- If generating code, prefer Tailwind classes over custom CSS.
- Generate Japanese text for UI elements by default, matching the site's language.

## 6. Directory Structure

```
/
├── assets/
│   ├── images/      # Static images (logos, icons)
│   └── (css/js)     # Future expansion
├── index.html       # Main entry point
├── README.md        # Project documentation
└── AGENTS.md        # This file
```

---
*Last Updated: 2026-02-16*
