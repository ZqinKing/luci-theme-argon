# AGENTS.md - luci-theme-argon

## Overview
This is a LuCI theme for OpenWrt, forked from upstream to fix bugs. It provides a modern, clean UI with light/dark mode support.

**Project Type**: OpenWrt LuCI Theme  
**Version**: 2.4.3  
**Test Environment**: http://10.0.0.252 (root/password)

---

## Build Commands

This project uses the OpenWrt build system. No npm/build scripts available.

### CSS Compilation
LESS files in `/less/` compile to `/htdocs/luci-static/argon/css/`:
```bash
# Manual compilation (if lessc is available)
lessc less/cascade.less htdocs/luci-static/argon/css/cascade.css
lessc less/dark.less htdocs/luci-static/argon/css/dark.css
```

### OpenWrt SDK Build
```bash
# Full build via OpenWrt SDK
make package/luci-theme-argon/{clean,compile} -j$(nproc)
```

---

## Code Style Guidelines

### LESS/CSS
- **Indentation**: 2 spaces
- **Quotes**: Double quotes for URLs/strings
- **Variables**: CSS custom properties in `:root` (e.g., `--primary: #5e72e4`)
- **Imports**: Use `@import url("file.less");` format
- **Nesting**: Supported via LESS, max 3 levels deep
- **Output**: First line of each `.less` file specifies output path:
  ```less
  // out: ../htdocs/luci-static/argon/css/cascade.css, compress: false
  ```

### JavaScript
- **Style**: ES5 compatible (LuCI runs on older browsers)
- **Indentation**: Tabs (follow existing files)
- **Strict Mode**: `'use strict';` at file start
- **Modules**: Use LuCI's module system:
  ```javascript
  'require baseclass';
  'require ui';
  return baseclass.extend({ ... });
  ```
- **Comments**: JSDoc for functions
- **No jQuery**: Use native DOM APIs (`document.querySelector`, etc.)

### ucode Templates (`.ut` files)
- **Syntax**: ucode template engine (similar to Jinja2)
- **Comments**: `{# comment #}`
- **Code blocks**: `{% code %}`
- **Output**: `{{ variable }}`
- **Conditionals**: `{% if (condition): %}...{% endif %}`

### File Organization
```
less/           # LESS source files
htdocs/         # Static web assets (CSS, JS, images)
ucode/          # ucode templates
themes/argon/   # Header/footer templates
root/           # System files (RPcd scripts, uci defaults)
```

---

## Error Handling

### JavaScript
- Check element existence before DOM operations
- Use `console.warn()` for missing elements
- Wrap callbacks in try-catch:
  ```javascript
  try {
    callback.call(element);
  } catch (e) {
    console.error('Error:', e);
  }
  ```

### CSS
- Use CSS custom properties with fallbacks:
  ```css
  color: #5e72e4;
  color: var(--primary);
  ```

---

## Testing

**No automated test framework detected.**

Manual testing process:
1. Build the theme package
2. Install on test router (or use test environment)
3. Verify in Chrome (recommended browser)
4. Test both light and dark modes
5. Test mobile responsiveness

---

## Important Notes

### Browser Support
- **Primary**: Chrome (best CSS3 compatibility)
- **Test**: Firefox, Safari
- **Not Supported**: Internet Explorer (officially retired)

### CSS Features Used
- CSS Custom Properties (variables)
- Flexbox layout
- CSS Grid
- `backdrop-filter` (blur effects)
- CSS transitions/animations

### Key Files
- `less/cascade.less` - Main stylesheet entry point
- `less/dark.less` - Dark mode overrides
- `htdocs/luci-static/resources/menu-argon.js` - Menu functionality
- `ucode/template/themes/argon/` - HTML templates

### Version Management
Update version in `Makefile`:
```makefile
PKG_VERSION:=2.4.3
PKG_RELEASE:=20250722
```

---

## External Rules
- No `.cursorrules` file found
- No `.cursor/rules/` directory
- No `.github/copilot-instructions.md`

---

## Fork Notes
This is a bug-fix fork of the upstream luci-theme-argon.
- Upstream: https://github.com/jerrykuku/luci-theme-argon
- Submit PRs to fix bugs only
- Follow existing code patterns strictly
