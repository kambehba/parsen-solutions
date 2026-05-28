# Blennd — SvelteKit 5 + TypeScript + Tailwind CSS v4

A pixel-faithful recreation of [blennd.com](https://blennd.com) using:

- **SvelteKit 2** (with **Svelte 5** runes syntax)
- **TypeScript** throughout
- **Tailwind CSS v4** (via `@tailwindcss/vite` plugin — no config file needed)
- **Google Fonts** — Syne (display) + DM Sans (body)

---

## Getting Started

### 1. Install dependencies

```bash
npm install
```

### 2. Run the dev server

```bash
npm run dev
```

Open [http://localhost:5173](http://localhost:5173).

### 3. Build for production

```bash
npm run build
npm run preview
```

---

## Svelte 5 Highlights

This project uses **Svelte 5 runes** exclusively:

| Feature | Syntax |
|---|---|
| Reactive state | `let x = $state(0)` |
| Derived values | `let y = $derived(x * 2)` |
| Props | `let { children } = $props()` |
| Slot replacement | `{@render children()}` |
| Event handlers | `onclick={fn}` (no `on:click`) |

---

## Tailwind v4 Notes

- No `tailwind.config.js` — configuration lives in `src/app.css` via `@theme { ... }`
- Plugin is `@tailwindcss/vite` added directly to `vite.config.ts`
- Custom brand tokens exposed as CSS variables and Tailwind utilities:
  - `bg-brand-accent`, `text-brand-black`, `border-brand-gray-light`, etc.
- Custom animations defined in `app.css`: `animate-marquee`, `animate-fade-up`, `animate-fade-in`

---

## Project Structure

```
src/
├── app.html              # HTML shell
├── app.css               # Tailwind + theme tokens + animations
├── routes/
│   ├── +layout.svelte    # Root layout (Nav + Footer)
│   └── +page.svelte      # Home page
└── lib/
    └── components/
        ├── Nav.svelte    # Responsive navigation with dropdowns
        └── Footer.svelte # Site footer
```
