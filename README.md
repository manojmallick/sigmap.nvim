<div align="center">

# sigmap.nvim

### SigMap AI context engine — Neovim plugin

[![GitHub release](https://img.shields.io/github/v/release/manojmallick/sigmap.nvim?color=7c6af7&label=release&logo=github)](https://github.com/manojmallick/sigmap.nvim/releases/latest)
[![License: MIT](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![Neovim ≥0.9](https://img.shields.io/badge/neovim-%E2%89%A50.9-57A143?logo=neovim)](https://neovim.io)
[![Node ≥18](https://img.shields.io/badge/node-%E2%89%A518-brightgreen?logo=node.js)](https://nodejs.org)

**80.0% retrieval hit@5 · 96.9% token reduction · 29 languages · Zero npm deps**

</div>

---

## What is SigMap?

SigMap extracts a compact **signature map** of your entire codebase — function names, class hierarchies, exported types — and writes it to `.github/copilot-instructions.md`. Every AI coding assistant reads that file as its first-message context.

This plugin brings SigMap into Neovim with commands, auto-run on save, a statusline widget, and `:checkhealth` integration.

```
Before SigMap: "I don't know your codebase — can you share some files?"
After SigMap:  "I can see your AuthService, UserRepository, 47 API routes…"
```

---

## What's new in v4.0

- Standalone release — independent version cycle from the SigMap CLI core
- Compatible with SigMap CLI v6.0 (graph-boosted retrieval, incremental sig cache)
- Install path corrected: `'manojmallick/sigmap.nvim'` (no `subdir` needed)

---

## Install

### lazy.nvim

```lua
{
  'manojmallick/sigmap.nvim',
  config = function()
    require('sigmap').setup({
      auto_run    = true,   -- regen on BufWritePost for source files
      float_query = true,   -- show query results in a floating window
    })
  end,
}
```

### packer.nvim

```lua
use {
  'manojmallick/sigmap.nvim',
  config = function()
    require('sigmap').setup({ auto_run = true })
  end,
}
```

### vim-plug

```vim
Plug 'manojmallick/sigmap.nvim'
```

Then in your Lua config:
```lua
require('sigmap').setup({ auto_run = true })
```

---

## Commands

| Command | Description |
|---|---|
| `:SigMap [args]` | Regenerate AI context file (passes `args` to the CLI) |
| `:SigMapQuery <text>` | TF-IDF ranked file retrieval in a floating window |

---

## Configuration

```lua
require('sigmap').setup({
  auto_run    = false,  -- regen on BufWritePost for *.js/ts/py/go/rs/java/rb/lua
  binary      = nil,    -- nil: auto-detect (sigmap → npx sigmap → local gen-context.js)
  notify      = true,   -- vim.notify on completion
  float_query = true,   -- show :SigMapQuery results in a floating window
})
```

---

## Statusline widget

Returns `sm:✓` when context is < 24 h old, `sm:⚠ Nh` otherwise.

### lualine

```lua
require('lualine').setup({
  sections = {
    lualine_x = { require('sigmap').statusline },
  },
})
```

### heirline / custom statusline

```lua
require('sigmap').statusline()
```

---

## Health check

```
:checkhealth sigmap
```

Validates:
- Node 18+ is installed
- `sigmap` binary (or `npx sigmap` / local `gen-context.js` fallback) is present
- Context file exists and is fresh (< 24 h)

---

## Requirements

| Requirement | Details |
|---|---|
| **Neovim** | 0.9 or higher |
| **Node.js** | 18 or higher |
| **SigMap CLI** | `npm install -g sigmap` or `npx sigmap` |

Binary auto-detection order: `sigmap` global → `npx sigmap` → local `gen-context.js`

---

## Benchmark

| Metric | Value |
|---|---:|
| Retrieval hit@5 | **80.0%** vs 13.6% baseline |
| Graph-boosted hit@5 | **83.3%** |
| Overall token reduction | **96.9%** |
| Prompt reduction | **40.8%** (2.84 → 1.68) |
| Languages supported | **29** |

---

## CLI quick reference

```bash
sigmap                    # generate once
sigmap ask "auth flow"    # query-focused context
sigmap validate           # check coverage
sigmap judge              # score answer groundedness
sigmap --watch            # auto-regen on file changes
sigmap --mcp              # start MCP server (9 tools)
```

---

## Links

| | |
|---|---|
| 📖 Docs | [manojmallick.github.io/sigmap](https://manojmallick.github.io/sigmap/) |
| 🔌 VS Code | [github.com/manojmallick/sigmap-vscode](https://github.com/manojmallick/sigmap-vscode) |
| 🧩 JetBrains | [github.com/manojmallick/sigmap-jetbrains](https://github.com/manojmallick/sigmap-jetbrains) |
| 🖥 CLI / core | [github.com/manojmallick/sigmap](https://github.com/manojmallick/sigmap) |
| 📦 npm | [npmjs.com/package/sigmap](https://www.npmjs.com/package/sigmap) |
| 🐛 Issues | [github.com/manojmallick/sigmap.nvim/issues](https://github.com/manojmallick/sigmap.nvim/issues) |

---

<div align="center">

MIT © 2026 [Manoj Mallick](https://github.com/manojmallick) · Made in Amsterdam 🇳🇱

</div>
