---
title: Installation
description: How to install dependencies and structure your app.
---

<script>
  import { Alert, AlertDescription } from "@/registry/default/ui/alert";
  import { Steps } from "$components/docs";
</script>

Unlike the original [shadcn/ui](https://ui.shadcn.com) for React, where the full components can exist in a single file, components in this port are split into multiple files. This is because Svelte doesn't support defining multiple components in a single file, so utilizing the CLI to add components will be the optimal approach.

The CLI will create a folder for _each_ component, which will sometimes just contain a single Svelte file, and in other times, multiple files. Within each folder, there will be an `index.ts` file that exports the component(s), so you can import them from a single file.

For example, the Accordion component is split into four `.svelte` files:

- `Accordion.svelte`
- `AccordionContent.svelte`
- `AccordionItem.svelte`
- `AccordionTrigger.svelte`

They can then be imported from the `accordion/index.ts` file like so:

```ts
import * as Accordion from '$components/ui/accordion"
// or
import {
  Accordion,
  AccordionContent,
  AccordionItem,
  AccordionTrigger
} from "$components/ui/accordion"
```

Regardless of the import approach you take, the components will be tree-shaken by Rollup, so you don't have to worry about unused components being bundled into your app.

## New Project

<Steps>

### Create project

Use the SvelteKit CLI to create a new project.

```bash
npm create svelte@latest my-app
```

### Add TailwindCSS

Use the `svelte-add` CLI to add Tailwind CSS to your project.

```bash
npx svelte-add@latest tailwindcss
```

### Install dependencies

```bash
npm install
```

### Run the CLI

```bash
npx shadcn-svelte@latest init
```

### Configure components.json

You will be asked a few questions to configure `components.json`:

```txt showLineNumbers
Which style would you like to use? › Default
Which color would you like to use as base color? › Slate
Where is your global CSS file? › src/app.postcss
Where is your tailwind.config.[cjs|js|ts] located? › tailwind.config.js
Configure the import alias for components: › $lib/components
Configure the import alias for utils: › $lib/utils
```

</Steps>

## Manual Installation

<Steps>

### Create project

Use the SvelteKit CLI to create a new project.

```bash
npm create svelte@latest my-app
```

### Add Tailwind

Use the `svelte-add` CLI to add Tailwind CSS to your project.

```bash
npx svelte-add@latest tailwindcss
```

### Add dependencies

Add the following dependencies to your project:

```bash
npm install tailwindcss-animate tailwind-variants clsx tailwind-merge
```

### Configure tailwind.config.js

This is what this project's `tailwind.config.js` file looks like:

```javascript title="tailwind.config.js"
import { fontFamily } from "tailwindcss/defaultTheme";
import tailwindcssAnimate from "tailwindcss-animate";

/** @type {import('tailwindcss').Config} */
const config = {
  darkMode: ["class"],
  content: ["./src/**/*.{html,js,svelte,ts}"],
  theme: {
    container: {
      center: true,
      padding: "2rem",
      screens: {
        "2xl": "1400px"
      }
    },
    extend: {
      colors: {
        border: "hsl(var(--border))",
        input: "hsl(var(--input))",
        ring: "hsl(var(--ring))",
        background: "hsl(var(--background))",
        foreground: "hsl(var(--foreground))",
        primary: {
          DEFAULT: "hsl(var(--primary))",
          foreground: "hsl(var(--primary-foreground))"
        },
        secondary: {
          DEFAULT: "hsl(var(--secondary))",
          foreground: "hsl(var(--secondary-foreground))"
        },
        destructive: {
          DEFAULT: "hsl(var(--destructive))",
          foreground: "hsl(var(--destructive-foreground))"
        },
        muted: {
          DEFAULT: "hsl(var(--muted))",
          foreground: "hsl(var(--muted-foreground))"
        },
        accent: {
          DEFAULT: "hsl(var(--accent))",
          foreground: "hsl(var(--accent-foreground))"
        },
        popover: {
          DEFAULT: "hsl(var(--popover))",
          foreground: "hsl(var(--popover-foreground))"
        },
        card: {
          DEFAULT: "hsl(var(--card))",
          foreground: "hsl(var(--card-foreground))"
        }
      },
      borderRadius: {
        lg: "var(--radius)",
        md: "calc(var(--radius) - 2px)",
        sm: "calc(var(--radius) - 4px)"
      },
      fontFamily: {
        sans: ["Inter", ...fontFamily.sans]
      }
    }
  },
  plugins: [tailwindcssAnimate]
};

export default config;
```

Feel free to add or modify as needed to suit your project.

### Configure styles

Add the following to your `src/app.postcss` file. You can learn more about using CSS variables for theming in the [theming section](/docs/theming).

```css title="src/app.postcss"
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  :root {
    --background: 0 0% 100%;
    --foreground: 222.2 47.4% 11.2%;

    --muted: 210 40% 96.1%;
    --muted-foreground: 215.4 16.3% 46.9%;

    --popover: 0 0% 100%;
    --popover-foreground: 222.2 47.4% 11.2%;

    --border: 214.3 31.8% 91.4%;
    --input: 214.3 31.8% 91.4%;

    --card: 0 0% 100%;
    --card-foreground: 222.2 47.4% 11.2%;

    --primary: 222.2 47.4% 11.2%;
    --primary-foreground: 210 40% 98%;

    --secondary: 210 40% 96.1%;
    --secondary-foreground: 222.2 47.4% 11.2%;

    --accent: 210 40% 96.1%;
    --accent-foreground: 222.2 47.4% 11.2%;

    --destructive: 0 92% 38%;
    --destructive-foreground: 210 40% 98%;

    --ring: 215 20.2% 65.1%;

    --radius: 0.5rem;
  }

  .dark {
    --background: 224 71% 4%;
    --foreground: 213 31% 91%;

    --muted: 223 47% 11%;
    --muted-foreground: 215.4 16.3% 56.9%;

    --accent: 216 34% 17%;
    --accent-foreground: 210 40% 98%;

    --popover: 224 71% 4%;
    --popover-foreground: 215 20.2% 65.1%;

    --border: 216 34% 17%;
    --input: 216 34% 17%;

    --card: 224 71% 4%;
    --card-foreground: 213 31% 91%;

    --primary: 210 40% 98%;
    --primary-foreground: 222.2 47.4% 1.2%;

    --secondary: 222.2 47.4% 11.2%;
    --secondary-foreground: 210 40% 98%;

    --destructive: 359 51% 48%;
    --destructive-foreground: 210 40% 98%;

    --ring: 216 34% 17%;

    --radius: 0.5rem;
  }
}

@layer base {
  * {
    @apply border-border;
  }
  body {
    @apply bg-background text-foreground;
    font-feature-settings: "rlig" 1, "calt" 1;
  }
}
```

### Add a cn helper

You'll want to create a `cn` helper to make it easier to conditionally add Tailwind CSS classes. This project defines it in `lib/utils.ts`:

```ts title="lib/utils.ts"
import type { ClassValue } from "clsx";
import { clsx } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}
```

### Import styles to your app

Create `src/routes/+layout.svelte` and import the styles:

```svelte title="src/routes/+layout.svelte"
<script lang="ts">
  import "../app.postcss";
</script>

<slot />
```

</Steps>

## Icons

This project uses icons from [Lucide](https://lucide.dev/), but feel free to use any icon library.

## App structure

Here's a recommended, but not required app structure:

```txt {4-11,15,19}
src
├── lib
│   ├── components
│   │   ├── ui
│   │   │   ├── alert-dialog
│   │   │   │   ├── index.ts
│   │   │   │   └── alert.svelte
│   │   │   ├── button
│   │   │   │   ├── index.ts
│   │   │   │   └── button.svelte
│   │   │   └── ...
│   │   ├── navigation.svelte
│   │   ├── page-header.svelte
│   │   └── ...
│   └── utils.ts
├── routes
│   ├── +page.svelte
│   └── +layout.svelte
├── app.postcss
```

- Place the UI components in the `lib/components/ui` folder.
- The rest of the components such as `<PageHeader />` and `<Navigation />` are placed in the `lib/components` folder.
- The `lib/utils.ts` file is where you can define the `cn` helper.
- The `app.postcss` file contains the global CSS.

That's it. You can now start adding components to your project.
