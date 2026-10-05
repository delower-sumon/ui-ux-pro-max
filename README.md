---
name: ui-ux-pro-max
description: "Comprehensive design guide for web and mobile applications. Contains 67 styles, 161 color palettes, 57 font pairings, 99 UX guidelines, and 25 chart types across 16 technology stacks."
---

# ui-ux-pro-max

Comprehensive design guide for web and mobile applications. Contains 67 styles, 161 color palettes, 57 font pairings, 99 UX guidelines, and 25 chart types across 16 technology stacks. Searchable database with priority-based recommendations.

# Prerequisites

Check if Python is installed:

```bash
python3 --version || python --version
```

If Python is not installed, install it based on user's OS:

**macOS:**
```bash
brew install python3
```

**Ubuntu/Debian:**
```bash
sudo apt update && sudo apt install python3
```

**Windows:**
```powershell
winget install Python.Python.3.12
```

---

## How to Use This Skill

Use this skill when the user requests any of the following:

| Scenario | Trigger Examples | Start From |
|----------|-----------------|------------|
| **New project / page** | "做一个 landing page"、"Build a dashboard" | Step 1 → Step 2 (design system) |
| **New component** | "Create a pricing card"、"Add a modal" | Step 3 (domain search: style, ux) |
| **Choose style / color / font** | "What style fits a fintech app?"、"推荐配色" | Step 2 (design system) |
| **Review existing UI** | "Review this page for UX issues"、"检查无障碍" | Quick Reference checklist above |
| **Fix a UI bug** | "Button hover is broken"、"Layout shifts on load" | Quick Reference → relevant section |
| **Improve / optimize** | "Make this faster" | Step 3 (domain search: ux, react) |
| **Implement dark mode** | "Add dark mode support" | Step 3 (domain: style "dark mode") |
| **Add charts / data viz** | "Add an analytics dashboard chart" | Step 3 (domain: chart) |
| **Stack best practices** | "React performance tips" | Step 4 (stack search) |

Follow this workflow:

### Step 1: Analyze User Requirements

Extract key information from user request:
- **Product type**: Entertainment, Tool, Productivity, Fintech, Healthcare, E-commerce, etc.
- **Target audience**: C-end or B-end, consider demographics.
- **Style keywords**: Modern, minimal, vibrant, dark mode, content-first, etc.
- **Stack**: HTML, Javascript, CSS, Python (current project).

### Step 2: Generate Design System (REQUIRED)

**Always start with `--design-system`** to get comprehensive recommendations with reasoning:

```bash
python3 skills/ui-ux-pro-max/scripts/search.py "<product_type> <industry> <keywords>" --design-system [-p "Project Name"]
```

This command:
1. Searches domains in parallel (product, style, color, landing, typography)
2. Applies reasoning rules from `ui-reasoning.csv` to select best matches
3. Returns complete design system: pattern, style, colors, typography, effects
4. Includes anti-patterns to avoid

**Example:**
```bash
python3 skills/ui-ux-pro-max/scripts/search.py "beauty spa wellness service" --design-system -p "Serenity Spa"
```

### Step 3: Supplement with Detailed Searches (as needed)

After getting the design system, use domain searches to get additional details:

```bash
python3 skills/ui-ux-pro-max/scripts/search.py "<keyword>" --domain <domain> [-n <max_results>]
```

**When to use detailed searches:**

| Need | Domain | Example |
|------|--------|---------|
| Product type patterns | `product` | `--domain product "fintech social"` |
| More style options | `style` | `--domain style "glassmorphism dark"` |
| Color palettes | `color` | `--domain color "vibrant"` |
| Font pairings | `typography` | `--domain typography "modern"` |
| Chart recommendations | `chart` | `--domain chart "dashboard"` |
| UX best practices | `ux` | `--domain ux "loading accessibility"` |
| Landing structure | `landing` | `--domain landing "hero"` |
| AI prompt / CSS keywords | `prompt` | `--domain prompt "minimalism"` |

### Step 4: Stack Guidelines

Get implementation-specific best practices:

```bash
python3 skills/ui-ux-pro-max/scripts/search.py "<keyword>" --stack <stack>
```

---

## Search Reference

### Available Domains

| Domain | Use For |
|--------|---------|
| `product` | Product type recommendations |
| `style` | UI styles, colors, effects |
| `typography` | Font pairings, Google Fonts |
| `color` | Color palettes by product type |
| `landing` | Page structure, CTA strategies |
| `chart` | Chart types, library recommendations |
| `ux` | Best practices, anti-patterns |
| `react` | React/Next.js performance |
| `web` | General web interface guidelines |
| `prompt` | AI prompts, CSS keywords |

### Available Stacks

Supported stacks include: `react`, `nextjs`, `vue`, `svelte`, `astro`, `swiftui`, `react-native`, `flutter`, `nuxt`, `nuxtui`, `tailwind`, `shadcn-ui`, `jetpack-compose`, `threejs`, `angular`, `laravel`, `html-tailwind`.

---

## Example Workflow

**User request:** "Build a dashboard for a finance app."

### Step 1: Analyze Requirements
- Product type: Fintech
- Style keywords: professional, clean, data-dense
- Stack: HTML / TailWind

### Step 2: Generate Design System (REQUIRED)

```bash
python3 skills/ui-ux-pro-max/scripts/search.py "fintech finance dashboard professional" --design-system -p "FinTrack"
```

**Output:** Complete design system.

### Step 3: Supplement with Detailed Searches

```bash
# Get chart types
python3 skills/ui-ux-pro-max/scripts/search.py "finance investment" --domain chart
```

---

## Tips for Better Results

- Use **multi-dimensional keywords**
- Add `--stack` for implementation-specific guidance
- Run `--domain ux` for a final review pass

---

## Dialogs & Confirmation Modal Standards (Zero Native Popups)

### 1. Absolute Prohibition of Browser-Native Dialogs
- **NEVER use browser-native dialogs**: `window.confirm()`, `window.alert()`, `window.prompt()`.
- Browser-native dialogs disrupt platform aesthetics, freeze UI threads, cannot be styled, and deliver a jarring experience.

### 2. Decision Matrix: Direct Action vs In-App Modal

| Action Type | Examples | Pattern to Apply |
|---|---|---|
| **Routine / Safe / Reversible** | Clear notifications, mark as read, toggle bookmark, filter reset | **No confirmation dialog.** Execute immediately with optimistic UI updates and toast feedback (`showToast("...", "info")`). |
| **Destructive / Irreversible** | Delete listing, cancel paid booking, purge account, payout transfer | **In-App Confirmation Popup Modal** with explicit title, context explanation, and cancel/action buttons. |

### 3. In-App Confirmation Modal Specification
When a confirmation is strictly needed:
- **Overlay**: Fixed inset with dark semi-transparent backdrop and subtle blur (`fixed inset-0 bg-black/50 backdrop-blur-xs z-[10000]`).
- **Container**: Elevated card with modern rounded geometry (`bg-white rounded-3xl shadow-2xl p-6 max-w-sm sm:max-w-md w-full animate-in fade-in zoom-in-95`).
- **Typography & Tone**: Plain, human title (e.g., "Request Payout") and succinct impact statement.
- **Buttons**:
  - Cancel button: Neutral muted pill (`px-4 py-2.5 rounded-xl border border-zinc-200 text-zinc-600 hover:bg-zinc-50 font-bold text-xs`).
  - Action button: Destructive / Theme colored pill (`px-5 py-2.5 rounded-xl bg-rose-600 hover:bg-rose-700 text-white font-bold text-xs shadow-xs`).
- **Keyboard & Accessibility**: Pressing `Escape` or clicking overlay cancels the action cleanly.

