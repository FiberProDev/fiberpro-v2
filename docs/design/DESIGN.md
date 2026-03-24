# Design System Specification: The Operational Architect

## 1. Overview & Creative North Star
**Creative North Star: The Silent Orchestrator**
In the high-stakes world of telecom permitting and traffic control, the UI must not compete for attention; it must facilitate focus. This design system moves beyond "SaaS-standard" by adopting an editorial, architectural approach. We replace the "boxed-in" feeling of traditional dashboards with a layout strategy driven by intentional whitespace and tonal depth. By prioritizing clear information density over decorative elements, we create a tool that feels less like a website and more like a high-precision instrument.

**Breaking the Template:**
We reject the heavy-handed use of borders and shadows. Instead, we use "Tonal Sculpting"—using subtle shifts in background values to define functional zones. This creates a "breathable" interface that reduces cognitive load during 8-hour operational shifts.

---

## 2. Colors & Surface Philosophy
The palette is rooted in a "cool-neutral" spectrum, designed to be easy on the eyes while providing enough contrast for critical data points.

### The "No-Line" Rule
**Explicit Instruction:** Do not use 1px solid borders (`outline`) to section off large areas of the UI. Structure must be achieved through background shifts. For example, a side navigation panel should use `surface-container-low` against a `surface` main content area. This "edge-to-edge" tonal transition creates a modern, sophisticated boundary without the visual "noise" of lines.

### Surface Hierarchy & Nesting
Treat the UI as a series of physical layers of fine paper. Use the surface-container tokens to communicate importance and nesting:
* **Base Layer:** `surface` (#f8f9fa) — The global canvas.
* **Secondary Zones:** `surface-container-low` (#f1f4f6) — Utility bars and navigation.
* **Primary Content Cards:** `surface-container-lowest` (#ffffff) — The highest importance data.
* **Nested Elements:** Use `surface-container-high` (#e3e9ec) for recessed areas within cards (e.g., a code snippet or a specific metadata block).

### The Glass & Signature Texture Rule
To elevate the "operational" feel to "premium," use **Glassmorphism** for floating elements like Modals or Toast notifications.
* **Implementation:** Use `surface` color at 80% opacity with a 12px backdrop-blur.
* **Signature Gradients:** For primary Call-to-Actions (CTAs), do not use a flat hex. Apply a subtle linear gradient from `primary` (#005bc1) to `primary_dim` (#004faa) at a 135-degree angle. This adds "soul" and depth to an otherwise clinical environment.

---

## 3. Typography: The Editorial Voice
We use **Inter** exclusively for its neutral, highly legible character. The hierarchy is designed to mimic a professional technical manual—authoritative and organized.

* **The Power Scale:**
* **Display (lg/md):** Reserved for high-level data dashboards (e.g., "42 Active Permits"). Use `on_surface` with `-0.02em` letter spacing for a "tight," custom look.
* **Headlines & Titles:** Used for page headers. Ensure a 24px (`spacing.6`) bottom margin to let the header breathe.
* **Body (md/sm):** The workhorse. Use `body-md` for standard forms and `body-sm` for dense data tables.
* **Labels (md/sm):** Always use `label-md` for input labels, rendered in `on_surface_variant` (#586064) to distinguish them from user input.

---

## 4. Elevation & Depth
Depth in this system is a result of light and layering, not artificial "drop shadows."

* **The Layering Principle:** A card should feel "lifted" simply by being `surface-container-lowest` (pure white) on top of a `surface` (light gray) background.
* **Ambient Shadows:** If a component must float (e.g., a dropdown menu), use a shadow with a blur of `24px` and a color of `rgba(43, 52, 55, 0.06)`. It should feel like a soft glow of light, not a dark stain.
* **The "Ghost Border" Fallback:** In rare cases where a border is required for accessibility (e.g., high-contrast mode or complex nested inputs), use `outline_variant` at **15% opacity**. A 100% opaque border is considered a design failure in this system.

---

## 5. Components & Data Patterns

### Buttons
* **Primary:** Gradient-filled (Primary to Primary-Dim), `rounded-md` (0.375rem). Use `on_primary` text.
* **Secondary:** `surface-container-high` background with `on_surface` text. No border.
* **Tertiary/Ghost:** No background. Use `primary` text color. Only shows a `surface-container-low` background on hover.

### Cards & Data Tables (The List Rule)
**Forbid the use of horizontal dividers.**
To separate list items or table rows, use a 4px vertical gap (`spacing.1`) or a subtle hover state shift to `surface-container-low`.
* **Columns:** Align numbers to the right; text to the left.
* **Padding:** Use `spacing.4` (1rem) as the minimum internal padding for any data container.

### Status Chips
Status is conveyed through "Soft Badges."
* **Structure:** A background of the status color (e.g., `error_container`) with text in the corresponding `on_error_container`.
* **Shape:** Use `rounded-full` for status indicators to contrast against the sharp, rectangular structure of the rest of the UI.

### Input Fields
* **Style:** `surface-container-lowest` background with a "Ghost Border" (15% `outline_variant`).
* **Focus State:** The border transitions to 100% `primary` with a 2px outer glow of `primary_fixed` at 30% opacity.

### Specialized Component: The Workflow Stepper
For telecom permits, use a "Minimalist Timeline" component. Avoid bulky circles. Use a 2px vertical line (`outline_variant` at 20%) with `label-sm` text. The active step is indicated by a single `primary` colored dot.

---

## 6. Do’s and Don’ts

### Do:
* **Do** use `spacing.8` (2rem) between major sections to emphasize the "High-End Editorial" feel.
* **Do** use `on_surface_variant` for metadata to create a clear visual hierarchy against primary text.
* **Do** align all elements to the defined 4px/8px spacing grid strictly.

### Don’t:
* **Don’t** use pure black (#000000) for text. Always use `on_surface` (#2b3437) to maintain the "Calm" feel.
* **Don’t** use shadows on buttons. They should feel integrated into the surface, not hovering above it.
* **Don’t** use "Alert Red" for everything negative. Use `error` (#9f403d) sparingly; it’s a professional tool, not a game.
* **Don't** use standard 1px dividers to separate items in a list. Use vertical whitespace (`spacing.3`) to define the rhythm.