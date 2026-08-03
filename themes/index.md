# Themes

Coder has two independent theming systems: a **UI theme** (the color palette used by the app's own chrome — sidebar, panels, menus, title bar) and an **editor theme** (the syntax-highlighting colors used by the Monaco code editor). They're set separately in **Settings → General** and can be mixed freely — there's no requirement that they match.

## UI Themes

Six built-in palettes, selectable from the **Theme** dropdown in Settings → General:

| Theme | Style |
|---|---|
| Coder Dark (Mocha) | Default — Catppuccin Mocha, purple/blue accent |
| Coder Light (Latte) | Catppuccin Latte, blue accent |
| Charcoal | Neutral, low-saturation dark gray (Cursor-style), monochrome/white accent |
| Charcoal Light | Light counterpart to Charcoal, same neutral character with a dark accent |
| Cappuccino | Warm dark (Sublime/Monokai-style), amber/orange accent |
| Cappuccino Light | Neutral warm-white counterpart to Cappuccino |

There's also a **System** option, which follows your OS's light/dark preference — but only ever resolves to Coder Dark or Coder Light, never Charcoal or Cappuccino, since there's no principled "system version" of a themed palette beyond the app's own default pair.

Switching takes effect immediately, no restart required. Your last choice is remembered on next launch with no flash of the wrong palette (a small cache of the resolved theme is applied before the app's UI even starts rendering).

## Editor Themes

Eight built-in Monaco themes, selectable from the **Editor theme** dropdown in Settings → General — completely independent of the UI theme above:

| Theme | Style |
|---|---|
| Coder Dark (Mocha) | Default — matches Catppuccin Mocha |
| Coder Light (Latte) | Matches Catppuccin Latte |
| Coder Macchiato | Alternate dark, warmer/lower contrast than Mocha |
| Coder Frappé | Softest/warmest dark, lowest contrast |
| Charcoal | Monochrome dark, matches the Charcoal UI theme |
| Charcoal Light | Monochrome light, matches Charcoal Light |
| Cappuccino | Monokai-style warm dark, matches the Cappuccino UI theme |
| Cappuccino Light | Neutral warm-white light, matches Cappuccino Light |

Each theme includes PHP-specific token color rules in addition to the generic ones, since Monaco's bundled PHP grammar emits its own token names that the generic rules alone don't match.

Switching the editor theme applies live to every open tab and the git diff viewer — no reopening files required.

The **integrated terminal** also follows the editor theme rather than the UI theme, since it's monospace/code-adjacent text — each editor theme has a matching 16-color terminal palette (hand-derived from that theme's own colors, since ANSI terminal colors aren't part of a Monaco theme). Switching applies live to every open terminal tab.

## Mix and match

Because the two systems are independent, you can run e.g. the **Charcoal** UI with the **Coder Dark (Mocha)** editor theme, or **Coder Light** UI with **Cappuccino** editor colors — whatever combination you prefer. The "coordinated" pairs (same name on both sides, like Charcoal ↔ Charcoal) are simply the sets that were designed to look like one cohesive system if you want that, not a requirement.

## Custom themes

Coder loads your own themes from `~/.coder/themes/` — **one folder per theme**, and the **folder name is the theme id** (shown as-is in the dropdowns, e.g. `themes/dracula/` → "dracula"):

```
~/.coder/themes/
  dracula/
    ui.css        UI (app-chrome) palette for "dracula"
    editor.json   Monaco editor theme for "dracula"
  nord/
    ui.css
    editor.json
```

- **UI**: `~/.coder/themes/<your-id>/ui.css` — a `:root { --var: value; ... }` block, same 15 variables as the built-in palettes (exact shape below). No `data-theme="..."` attribute needed on the selector — the folder name already is the id.
- **Editor**: `~/.coder/themes/<your-id>/editor.json` — a Monaco `IStandaloneThemeData` object (exact shape below).

Either file can exist without the other — a theme can be UI-only, editor-only, or both. There's no requirement that the two halves under one folder actually match stylistically; that's just where the convenience of "one id, one folder" comes from.

Custom themes appear in a separate **Custom** group at the bottom of the Theme / Editor theme dropdowns in Settings → General, once at least one is loaded.

**Rescanned when Settings opens** — not file-watched. Edit a file on disk, then reopen (or re-focus) Settings → General to pick up the change; no app restart needed. A theme that fails validation is skipped and reported as a toast notification (e.g. missing CSS variables, invalid Monaco theme shape) rather than breaking the rest of your custom set or the app.

What follows is the exact variable/JSON shape a custom theme needs to match — the same shape the built-in themes use.

### UI theme variables

A UI theme is exactly these 15 CSS custom properties, declared inside a plain `:root { ... }` block — no `data-theme="..."` attribute needed, since the folder name is already the id. All 15 are required — there's no partial-override/fallback-to-default behavior today. Values shown are Coder Dark (Mocha):

```css
/* ~/.coder/themes/your-theme-id/ui.css */
:root {
  --bg-base: #1e1e2e;       /* main background */
  --bg-surface: #181825;    /* sidebar, panels */
  --bg-overlay: #313244;    /* inputs, cards, raised surfaces */
  --bg-hover: #45475a;      /* hover state background */
  --border: #313244;        /* all borders/dividers */
  --text-primary: #cdd6f4;  /* main text */
  --text-secondary: #a6adc8;/* secondary/label text */
  --text-muted: #898b98;    /* placeholder/disabled text */
  --accent: #89b4fa;        /* links, active states, primary buttons */
  --accent-dim: #1e3a5f;    /* accent at low emphasis (e.g. selected-row bg) */
  --green: #a6e3a1;         /* success / added */
  --red: #f38ba8;           /* error / removed */
  --dark-red: #bb1041;      /* destructive-action emphasis */
  --yellow: #f9e2af;        /* warning */
  --mauve: #cba6f7;         /* secondary accent */
}
```

The selector itself (`:root`) is never actually read — only the declarations inside `{ }` matter, the folder name is still what determines the theme's id. `:root` is just the conventional, always-valid choice so the file lints clean in any editor.

Three layout variables (`--titlebar-height`, `--sidebar-width`, `--chat-width`) are **not** part of a theme — they're structural, shared by every palette.

### Editor theme JSON

An editor theme is a Monaco `IStandaloneThemeData` object — `base` (`'vs-dark'` or `'vs'`), `inherit: true`, a `rules` array of token→color mappings, and a `colors` map of editor chrome colors:

```json
{
  "base": "vs-dark",
  "inherit": true,
  "rules": [
    { "token": "comment", "foreground": "6c7086", "fontStyle": "italic" },
    { "token": "keyword", "foreground": "cba6f7" },
    { "token": "string", "foreground": "a6e3a1" },
    { "token": "number", "foreground": "fab387" },
    { "token": "type", "foreground": "89dceb" },
    { "token": "class", "foreground": "f9e2af" },
    { "token": "function", "foreground": "89b4fa" },
    { "token": "variable", "foreground": "cdd6f4" },
    { "token": "operator", "foreground": "89dceb" },
    { "token": "key", "foreground": "89dceb" },

    { "token": "variable.php", "foreground": "eba0ac" },
    { "token": "variable.predefined.php", "foreground": "ff306b", "fontStyle": "bold" },
    { "token": "identifier.php", "foreground": "cdd6f4" },
    { "token": "function-call.php", "foreground": "89b4fa" },
    { "token": "keyword.php", "foreground": "cba6f7" },
    { "token": "constant.php", "foreground": "fab387" },
    { "token": "string.php", "foreground": "a6e3a1" },
    { "token": "string.escape.php", "foreground": "94e2d5" },
    { "token": "number.php", "foreground": "fab387" },
    { "token": "number.float.php", "foreground": "fab387" },
    { "token": "number.hex.php", "foreground": "fab387" },
    { "token": "number.octal.php", "foreground": "fab387" },
    { "token": "number.binary.php", "foreground": "fab387" },
    { "token": "comment.php", "foreground": "6c7086", "fontStyle": "italic" },
    { "token": "delimiter.php", "foreground": "9399b2" },
    { "token": "delimiter.bracket.php", "foreground": "cdd6f4" },
    { "token": "delimiter.array.php", "foreground": "cdd6f4" },
    { "token": "delimiter.parenthesis.php", "foreground": "cdd6f4" },
    { "token": "metatag.php", "foreground": "f9e2af" }
  ],
  "colors": {
    "editor.background": "#1e1e2e",
    "editor.foreground": "#cdd6f4",
    "editorLineNumber.foreground": "#45475a",
    "editorLineNumber.activeForeground": "#a6adc8",
    "editor.selectionBackground": "#313244",
    "editor.inactiveSelectionBackground": "#27273a",
    "editorCursor.foreground": "#f5c2e7",
    "editor.lineHighlightBackground": "#24273a",
    "editorIndentGuide.background1": "#313244",
    "editorIndentGuide.activeBackground1": "#45475a",
    "editorBracketMatch.background": "#313244",
    "editorBracketMatch.border": "#89b4fa",
    "scrollbarSlider.background": "#31324488",
    "scrollbarSlider.hoverBackground": "#45475a88"
  }
}
```

The `*.php` rules exist because Monaco's bundled PHP grammar emits its own token names (`variable.php`, `keyword.php`, etc.) instead of matching the generic ones above it — without them, PHP code falls back to plain foreground for variables, property/method names, and punctuation. Every other token type (`comment`, `keyword`, `string`, …) works across all languages via Monaco's generic Monarch token names.

[← Back to Docs](/docs/index.md)
