# 🌙 tailwind-dark-theme

[![GitHub release](https://img.shields.io/github/v/release/alaa-abdallah1/tailwind-dark-theme.svg)](https://github.com/alaa-abdallah1/tailwind-dark-theme/releases)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue)](LICENSE)
[![NPM Package](https://img.shields.io/npm/v/tailwind-dark-theme?color=red)](https://www.npmjs.com/package/tailwind-dark-theme)
[![NPM downloads](https://img.shields.io/npm/dw/tailwind-dark-theme?color=limegreen)](https://www.npmjs.com/package/tailwind-dark-theme)

> **Powered by [Payiano Team](https://payiano.com) | [GitHub](https://github.com/payiano)**

A powerful Tailwind CSS plugin that provides **automatic dark/light theme switching** with inverted color schemes and custom theme variables.

⚡ **Automatic Color Inversion**: Dark theme automatically inverts Tailwind colors (white ↔ black, gray-50 ↔ gray-950, etc.) providing **seamless theme transitions**.

⚡ **Custom Theme Variables**: Define custom color variables for both light and dark modes with **flexible configuration** that integrates perfectly with your design system.

⚡ **Zero Configuration**: Works out of the box with sensible defaults while offering **extensive customization** options for advanced use cases.

⚡ **Selective Dark Mode**: Use `darkless` class to prevent dark mode application in specific areas, giving you **granular control** over your theming.

## Compatibility

Tested with Node 20+, Tailwind CSS 3.0+ and modern build tools. Compatible with Vite, Webpack, and other bundlers that support Tailwind CSS plugins.

## Installation

Install the plugin from [npm](https://www.npmjs.com/package/tailwind-dark-theme) with your preferred package manager:

```bash
# NPM
npm install tailwind-dark-theme

# Yarn
yarn add tailwind-dark-theme

# PNPM
pnpm add tailwind-dark-theme
```

[![NPM](https://nodei.co/npm/tailwind-dark-theme.png)](https://www.npmjs.com/package/tailwind-dark-theme)

## Usage

### Basic Setup

Import and use the `getTailwindConfig` function in your `tailwind.config.js`:

```javascript
import { getTailwindConfig } from "tailwind-dark-theme";

export default getTailwindConfig();
```

Enable dark mode by adding the `dark` class to your HTML or body element:

```html
<!DOCTYPE html>
<html class="dark">
  <head>
    <title>My App</title>
  </head>
  <body>
    <!-- Your app content -->
  </body>
</html>
```

Or toggle it dynamically:

```javascript
// Enable dark mode
document.documentElement.classList.add("dark");

// Disable dark mode
document.documentElement.classList.remove("dark");
```

### Advanced Configuration

You can customize the plugin with both standard Tailwind config and extended theme options:

```javascript
import { getTailwindConfig, TwMainColorVariants } from "tailwind-dark-theme";

export default getTailwindConfig(
  // Standard Tailwind CSS configuration
  {
    content: ["./src/**/*.{js,ts,jsx,tsx,vue}"],
    theme: {
      extend: {
        fontFamily: {
          sans: ["Inter", "sans-serif"],
        },
      },
    },
  },
  // Extended theme configuration
  {
    lightVars: {
      "--color-primary": "#3b82f6",
      "--bg-primary": "#3b82f6",
    },
    darkVars: {
      "--color-primary": "#60a5fa",
      "--bg-primary": "#60a5fa",
    },
    lightMainColor: TwMainColorVariants.slate,
    darkMainColor: TwMainColorVariants.zinc,
  }
);
```

See the [API Reference](#api-reference) section for detailed configuration options.

## API Reference

### `getTailwindConfig(config?, extended?)`

Generates a complete Tailwind CSS configuration with theme support.

#### Parameters

**`config`** _(optional)_: `Partial<Config>`

- Standard Tailwind CSS configuration object
- All standard Tailwind options are supported
- Your custom configuration will be merged with the theme defaults

**`extended`** _(optional)_: `ITwExtendedType`

- Extended theme configuration for custom colors and variables
- Allows customization of light/dark theme colors and main color variants

#### Returns

A complete Tailwind CSS configuration object ready to be exported.

## Extended Configuration (`ITwExtendedType`)

```typescript
interface ITwExtendedType {
  lightVars?: TwColors; // Custom variables for light theme
  darkVars?: TwColors; // Custom variables for dark theme
  lightMainColor?: TwMainColorVariants; // Main color variant for light theme
  darkMainColor?: TwMainColorVariants; // Main color variant for dark theme
}
```

### Properties

- **`lightVars`**: Custom color variables for light theme. Values can be any valid CSS color format (`#ffffff`, `white`, `hsl(0, 0%, 100%)`) or CSS variable references. **Important**: Variable names must start with `--color-` or `--bg-` prefix.

- **`darkVars`**: Custom color variables for dark theme. Similar to `lightVars`, these can be any valid color format or CSS variable references. **Important**: Variable names must start with `--color-` or `--bg-` prefix.

- **`lightMainColor`**: Main color variant for light theme. Must be one of: `gray`, `zinc`, `stone`, `slate`, `neutral`.

- **`darkMainColor`**: Main color variant for dark theme. Must be one of: `gray`, `zinc`, `stone`, `slate`, `neutral`.

### CSS Variable Naming Convention

When defining custom variables in `lightVars` and `darkVars`, you must use specific prefixes:

- **`--color-`** prefix: For text colors and general color variables
- **`--bg-`** prefix: For background colors

This naming convention is required because:

1. **Direct CSS Generation**: Variables are used exactly as defined to generate CSS
2. **Tailwind Integration**: Ensures variables work seamlessly with Tailwind's color system
3. **Type Specificity**: Clearly distinguishes between color and background usage
4. **Avoiding Conflicts**: Prevents naming conflicts with existing CSS variables

**Examples of correct variable names:**

- `--color-primary` - For text color usage
- `--bg-primary` - For background color usage
- `--color-success-DEFAULT` - For default success text color
- `--bg-error-700` - For error background shade 700

## Usage Examples

### Basic Usage

```javascript
// tailwind.config.js
import { getTailwindConfig } from "tailwind-dark-theme";

export default getTailwindConfig();
```

### Custom Tailwind Configuration

```javascript
// tailwind.config.js
import { getTailwindConfig } from "tailwind-dark-theme";

export default getTailwindConfig({
  content: [
    "./src/**/*.{js,ts,jsx,tsx,vue}",
    "./pages/**/*.{js,ts,jsx,tsx,vue}",
  ],
  theme: {
    extend: {
      fontFamily: {
        sans: ["Inter", "sans-serif"],
      },
      spacing: {
        18: "4.5rem",
      },
    },
  },
});
```

### Extended Theme Configuration

```javascript
// tailwind.config.js
import { getTailwindConfig, TwMainColorVariants } from "tailwind-dark-theme";

export default getTailwindConfig(
  {
    content: ["./src/**/*.{js,ts,vue}"],
  },
  {
    // Custom variables for light theme
    lightVars: {
      "--color-primary": "#3b82f6", // Primary text color
      "--bg-primary": "#3b82f6", // Primary background color
      "--color-secondary": "#10b981", // Secondary text color
      "--bg-secondary": "#10b981", // Secondary background color
      "--color-accent": "#f59e0b", // Accent text color
      "--bg-accent": "#f59e0b", // Accent background color
      "--color-surface": "#ffffff", // Surface text color
      "--bg-surface": "#ffffff", // Surface background color
      "--color-on-surface": "#1f2937", // Text on surface color
      "--bg-header": "#ffffff", // Header background
      "--bg-sidebar": "#f8fafc", // Sidebar background
    },
    // Custom variables for dark theme
    darkVars: {
      "--color-primary": "#60a5fa", // Primary text color (dark)
      "--bg-primary": "#60a5fa", // Primary background color (dark)
      "--color-secondary": "#34d399", // Secondary text color (dark)
      "--bg-secondary": "#34d399", // Secondary background color (dark)
      "--color-accent": "#fbbf24", // Accent text color (dark)
      "--bg-accent": "#fbbf24", // Accent background color (dark)
      "--color-surface": "#1f2937", // Surface text color (dark)
      "--bg-surface": "#1f2937", // Surface background color (dark)
      "--color-on-surface": "#f9fafb", // Text on surface color (dark)
      "--bg-header": "#0f172a", // Header background (dark)
      "--bg-sidebar": "#1e293b", // Sidebar background (dark)
    },
    // Main color variants
    lightMainColor: TwMainColorVariants.slate,
    darkMainColor: TwMainColorVariants.zinc,
  }
);
```

### Real-world Example with Color Constants

```javascript
// Using with color constants (like DEFAULT_COLORS)
import { getTailwindConfig } from "tailwind-dark-theme";
import { DEFAULT_COLORS } from "./colors";

export default getTailwindConfig(
  {
    content: ["./src/**/*.{js,ts,vue}"],
  },
  {
    lightVars: {
      "--bg-error-500": DEFAULT_COLORS.error[500],
      "--bg-success-500": DEFAULT_COLORS.success[500],
      "--color-success-DEFAULT": DEFAULT_COLORS.success.DEFAULT,
      "--color-warning-700": DEFAULT_COLORS.warning[700],
      "--bg-neutral-50": DEFAULT_COLORS.neutral[50],
    },
    darkVars: {
      "--bg-error-700": DEFAULT_COLORS.error[700],
      "--bg-success-700": DEFAULT_COLORS.success[700],
      "--color-success-DEFAULT": DEFAULT_COLORS.success[400],
      "--color-warning-400": DEFAULT_COLORS.warning[400],
      "--bg-neutral-950": DEFAULT_COLORS.neutral[950],
    },
  }
);
```

````

### Using Custom Variables in CSS

After defining custom variables with proper prefixes, you can use them directly in your CSS:

```css
/* Use the variables directly as defined */
.my-component {
  color: var(--color-primary);           /* Text color */
  background-color: var(--bg-primary);   /* Background color */
  border-color: var(--color-accent);     /* Border color */
}

/* Header styling */
.header {
  background-color: var(--bg-header);
  color: var(--color-on-surface);
}

/* Use with Tailwind utilities */
.text-primary {
  color: var(--color-primary);
}

.bg-surface {
  background-color: var(--bg-surface);
}
````

**Variable Usage Pattern:**

- Use variables exactly as you defined them in `lightVars`/`darkVars`
- `--color-*` variables for text colors and general color usage
- `--bg-*` variables for background colors

## Color Inversion

The plugin automatically inverts Tailwind's default color palette in dark mode:

| Light Mode | Dark Mode  |
| ---------- | ---------- |
| `white`    | `black`    |
| `gray-50`  | `gray-950` |
| `gray-100` | `gray-900` |
| `gray-200` | `gray-800` |
| `...`      | `...`      |
| `gray-900` | `gray-100` |
| `gray-950` | `gray-50`  |
| `black`    | `white`    |

This applies to all color variants (red, blue, green, etc.) and their numeric scales.

## Dark Mode Controls

### Global Dark Mode

```html
<!-- Enable dark mode globally -->
<html class="dark">
  <body>
    <!-- All content will use dark theme -->
  </body>
</html>
```

### Preventing Dark Mode in Specific Areas

Use the `darkless` class to prevent dark mode application in specific components:

```html
<div class="dark">
  <!-- This section uses dark theme -->
  <div class="bg-gray-900 text-white">Dark themed content</div>

  <!-- This section stays in light theme -->
  <div class="darkless bg-white text-black">Always light themed content</div>
</div>
```

### Dynamic Theme Switching

```javascript
// Theme toggle function
function toggleTheme() {
  const html = document.documentElement;
  const isDark = html.classList.contains("dark");

  if (isDark) {
    html.classList.remove("dark");
    localStorage.setItem("theme", "light");
  } else {
    html.classList.add("dark");
    localStorage.setItem("theme", "dark");
  }
}

// Initialize theme from localStorage
function initTheme() {
  const savedTheme = localStorage.getItem("theme");
  const prefersDark = window.matchMedia("(prefers-color-scheme: dark)").matches;

  if (savedTheme === "dark" || (!savedTheme && prefersDark)) {
    document.documentElement.classList.add("dark");
  }
}

// Call on page load
initTheme();
```

### React/Vue Theme Hook Example

```javascript
// React Hook
import { useState, useEffect } from "react";

export function useTheme() {
  const [isDark, setIsDark] = useState(false);

  useEffect(() => {
    const savedTheme = localStorage.getItem("theme");
    const prefersDark = window.matchMedia(
      "(prefers-color-scheme: dark)"
    ).matches;
    const shouldBeDark = savedTheme === "dark" || (!savedTheme && prefersDark);

    setIsDark(shouldBeDark);
    document.documentElement.classList.toggle("dark", shouldBeDark);
  }, []);

  const toggleTheme = () => {
    const newIsDark = !isDark;
    setIsDark(newIsDark);
    document.documentElement.classList.toggle("dark", newIsDark);
    localStorage.setItem("theme", newIsDark ? "dark" : "light");
  };

  return { isDark, toggleTheme };
}
```

## Complete Example

Here's a complete example showing all features:

```javascript
// tailwind.config.js
import { getTailwindConfig, TwMainColorVariants } from "tailwind-dark-theme";

export default getTailwindConfig(
  {
    content: ["./index.html", "./src/**/*.{js,ts,jsx,tsx,vue}"],
    theme: {
      extend: {
        fontFamily: {
          sans: ["Inter", "sans-serif"],
        },
        colors: {
          brand: {
            50: "#eff6ff",
            500: "#3b82f6",
            900: "#1e3a8a",
          },
        },
      },
    },
  },
  {
    lightVars: {
      "--color-header": "#1e293b", // Header text color
      "--bg-header": "#ffffff", // Header background color
      "--color-sidebar": "#64748b", // Sidebar text color
      "--bg-sidebar": "#f8fafc", // Sidebar background color
      "--color-content": "#1e293b", // Content text color
      "--bg-content": "#ffffff", // Content background color
      "--color-border": "#e2e8f0", // Border color
      "--color-text-primary": "#1e293b", // Primary text color
      "--color-text-secondary": "#64748b", // Secondary text color
    },
    darkVars: {
      "--color-header": "#f1f5f9", // Header text color (dark)
      "--bg-header": "#0f172a", // Header background color (dark)
      "--color-sidebar": "#94a3b8", // Sidebar text color (dark)
      "--bg-sidebar": "#1e293b", // Sidebar background color (dark)
      "--color-content": "#f1f5f9", // Content text color (dark)
      "--bg-content": "#0f172a", // Content background color (dark)
      "--color-border": "#334155", // Border color (dark)
      "--color-text-primary": "#f1f5f9", // Primary text color (dark)
      "--color-text-secondary": "#94a3b8", // Secondary text color (dark)
    },
    lightMainColor: TwMainColorVariants.slate,
    darkMainColor: TwMainColorVariants.slate,
  }
);
```

```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>My App</title>
  </head>
  <body>
    <div id="app">
      <!-- Header (always dark theme) -->
      <header class="darkless bg-gray-900 text-white p-4">
        <h1>My App</h1>
        <button onclick="toggleTheme()" class="bg-blue-500 px-4 py-2 rounded">
          Toggle Theme
        </button>
      </header>

      <!-- Main content (respects theme) -->
      <main class="bg-white dark:bg-gray-900 text-black dark:text-white p-6">
        <div class="bg-gray-100 dark:bg-gray-800 p-4 rounded">
          <h2>This content changes with theme</h2>
          <p class="text-gray-600 dark:text-gray-300">
            Background and text colors automatically invert in dark mode.
          </p>
        </div>

        <!-- Card with custom variables -->
        <div
          style="background-color: var(--bg-content); border-color: var(--color-border);"
          class="border p-4 rounded mt-4"
        >
          <h3 style="color: var(--color-text-primary)">Custom themed card</h3>
          <p style="color: var(--color-text-secondary)">
            Using custom CSS variables with proper prefixes
          </p>

          <!-- Example showing both color and background variable usage -->
          <div
            style="background-color: var(--bg-header); color: var(--color-header);"
            class="p-2 rounded mt-2"
          >
            Header-styled section using --bg-header and --color-header
          </div>
        </div>
      </main>
    </div>

    <script>
      function toggleTheme() {
        document.documentElement.classList.toggle("dark");
      }
    </script>
  </body>
</html>
```

## Contributing

Contributions are welcome! Please open issues or pull requests if you want to suggest improvements or fixes.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Code of Conduct

This project follows the [Contributor Code of Conduct](CODE-OF-CONDUCT.md). By participating, you agree to abide by its terms.

## Sponsoring

If you find this project helpful, please consider supporting me on Buy Me a Coffee! Your support helps me continue developing open-source software.

[![Buy Me A Coffee](https://cdn.buymeacoffee.com/buttons/default-orange.png)](https://buymeacoffee.com/alaa_abdallah1)
