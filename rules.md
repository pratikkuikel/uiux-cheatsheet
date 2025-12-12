# AI Agent Website Audit Rules & Instructions

This document outlines the standard operating procedure for an AI agent (Antigravity/Boost) to audit a website's UI/UX. The audit is based on the "UI/UX Cheatsheet" principles and includes specific instructions for Laravel applications.

## I. Route Discovery & Traversal

Before checking for UI/UX compliance, you must identify the pages to visit.

1.  **Laravel Route Identification**:
    *   **File Inspection**: Read the route definition files in the `routes/` directory. specifically look for `routes/web.php` or custom files like `routes/broccoli.php`.
    *   **Artisan Command**: Run the following command to get a comprehensive list of registered routes:
        ```bash
        php artisan route:list
        ```
    *   **Route Filtering**: Focus on `GET` routes that return HTML views (exclude API routes or pure redirection routes unless relevant).
    *   **Context**: If the application requires authentication, ensure you have a mechanism to visit protected routes (e.g., login first or use a test user).

2.  **Navigation**:
    *   The website can be accessed using the url {website}.test no need to run the artisan php server.
    *   Visit the identified routes.
    *   For each route, analyze the rendered DOM/UI against the rules below.

## II. UI/UX Compliance Rules

You are to check every page against the following strict rules. For every violation, note it as a **Defiance** and provide an **Improvement Suggestion**.

### A. The "Fix 90%" Core Rules
1.  **Spacing System**:
    *   **Rule**: All spacing (margins, padding, gaps) must follow an 8px grid (8, 16, 24, 32, 48px).
    *   **Check**: Are elements arbitrarily spaced (e.g., 13px, 7px)?
2.  **Reduction**:
    *   **Rule**: Reduce everything until nothing breaks to lower cognitive load.
    *   **Check**: Are there non-essential decorative elements cluttering the screen?
3.  **Color Hierarchy**:
    *   **Rule**: Use one primary color, one accent, and neutral greys.
    *   **Check**: Are there too many competing colors? Is the brand color overused?
4.  **Visual Hierarchy**:
    *   **Rule**: Every page must have a clear hierarchy (Top→Down, Left→Right).
    *   **Check**: Is the most important element the most prominent?
5.  **Button Discipline**:
    *   **Rule**: Only 3 button types: **Primary** (Main Action), **Secondary** (Alternative), **Destructive** (Negative action).
    *   **Check**: Are there more than 3 button styles? Is there more than one "Primary" button per view?
6.  **Alignment**:
    *   **Rule**: Everything must be aligned to an invisible grid.
    *   **Check**: Do elements look slightly off-center or misaligned vertically/horizontally?
7.  **Label Clarity**:
    *   **Rule**: Clear labels > Clever labels.
    *   **Check**: Is the copy ambiguous? (e.g., "Do it" instead of "Submit").
8.  **Grouping**:
    *   **Rule**: Use whitespace to group related items (Law of Proximity).
    *   **Check**: Are related items too far apart? Are unrelated items too close?
9.  **Micro-interactions**:
    *   **Rule**: Provide feedback for actions (hover, click, submit).
    *   **Check**: Does the interface feel static or dead when interacted with?
10. **Consistency**:
    *   **Rule**: Component re-usability is key.
    *   **Check**: Do similar elements look different on different pages?

### B. Typography
*   **Fonts**: Limit to 1–2 font families maximally.
*   **Base Size**: Body text should be ~16px. Headings should scale (20–28px+).
*   **Line Height**: Paragraphs must have 1.4–1.6 line height for readability.
*   **Hierarchy**: Use size/weight/color to denote importance, not decoration.

### C. Color Strategy
*   **Semantic Colors**: Green = Success, Red = Error, Yellow = Warning. Do not misuse them.
*   **Soft Extremes**: Avoid pure Black (#000) and pure White (#FFF). Use soft greys/off-whites to reduce eye strain.

### D. Emotional Design
*   **Onboarding**: Must show progress and feel fast (skeletons/optimistic UI).
*   **Microcopy**: Be friendly. "Saved successfully 🎉" > "Update completed".
*   **Empty States**: Never leave a blank container. Show [Icon + Short Copy + Call to Action].
*   **Success**: Make success states rewarding (confetti, toast, animations).
*   **Errors**: Guide, don't scold. Explain *how* to fix the error.

### E. Layout Patterns
*   **SaaS Standard**: Header → Sidebar → Content → (Optional Right Panel).
*   **Cards**: Use card-based grouping for lists and metrics.
*   **Singular Focus**: One primary action per screen.

### F. Accessibility (Non-Negotiable)
*   **Contrast**: Text must meet WCAG AA (4.5:1 ratio).
*   **Keyboard**: Focus states must be visible.
*   **Touch**: Interactive targets must be at least 44x44px.

### G. UX Laws Checklist
*   **Jakob’s Law**: Does it work like other familiar apps (e.g., Stripe, Slack)?
*   **Hick’s Law**: Are there too many choices? (Reduce complexity).
*   **Fitts’ Law**: Are important buttons large and easy to click?
*   **Miller’s Law**: is content chunked into groups (~7 items max)?
*   **Doherty Threshold**: Does the system respond <400ms (or use loaders)?
*   **Peak-End Rule**: Are the final steps of a flow delightful?

## III. The 7 Deadly Sins (Fail immediately if found)
1.  Too many colors.
2.  Inconsistent spacing.
3.  Cluttered layouts.
4.  Fancy text for no reason.
5.  Unclear buttons.
6.  Missing states (loading/error/empty).
7.  Prioritizing "creativity" over functionality.

## IV. Reporting Format

Write the report to violations.md file.

For each URL/Route audited, generate a report in the following format:

**Route:** `/example-path`

| Status | Rule ID | Observation | Improvement Suggestion |
| :--- | :--- | :--- | :--- |
| 🔴 **Defiance** | A.1 (Spacing) | Margin between Header and Content is 13px. | Change margin to 16px to align with 8px grid. |
| 🔴 **Defiance** | D.3 (Empty State) | Product table is empty with no message. | Add an empty state component with "Add Product" button. |
| 🟡 **Warning** | B (Typography) | Header font size is 18px (too small). | Increase header size to 24px+ for better hierarchy. |
| ✅ **Pass** | C (Color) | Primary buttons use consistent brand color. | N/A |

---
**Summary of Audited Routes:**
*   [Route 1] - [Score/Grade]
*   [Route 2] - [Score/Grade]
