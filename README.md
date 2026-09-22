# copyparty-ui

A modern, Google Drive-style web interface for [copyparty](https://github.com/9001/copyparty) — the powerful self-hosted file server.

copyparty's built-in UI is functional but dense. This project replaces it with a clean, familiar interface while keeping copyparty as the backend for all file operations. It ships as a standard Python package — install the wheel and run it with `python -m copyparty_ui`.

> This repository was generated using Claude Code, similar to https://github.com/opticsraybender/zosapi-autocomplete.

---

## Features

| Feature | Details |
|---|---|
| **File browser** | List and grid views, sortable columns, breadcrumb navigation |
| **Uploads** | Drag-and-drop anywhere on the page, click to pick, chunked parallel uploads (up2k protocol), per-file progress |
| **Downloads** | Single file or multi-select zip |
| **Search** | Filename search (copyparty index) + full-text content search (FTS5, built-in) |
| **Document viewers** | PDF, Word (.docx), Excel (.xlsx/.csv), PowerPoint (.pptx), Markdown, plain text |
| **Audio player** | Floating player with playlist, seek, volume |
| **Labels** | Gmail-style colored labels on files — create, assign, filter |
| **Filters** | Filter by label or file extension, persists across folder navigation |
| **Share links** | Create time-limited, password-protected share links via copyparty |
| **Context menu** | Right-click with Rename, Download, Delete, Labels, Open With |
| **Keyboard nav** | Arrow keys, Enter, Space, Ctrl+A, Delete, Shift+click range select |
| **Browser history** | Back/forward navigation via `pushHistory` |
| **Admin** | Trigger re-index, manage share links |
| **Network** | Accessible from the local network — not just localhost |

---

## Requirements

- **Windows** (paths and defaults are Windows-specific — `%USERPROFILE%`, `%LOCALAPPDATA%`)
- **Python 3.10+**
- Optional: `pillow` + `python-pptx` for PowerPoint slide rendering (`pip install copyparty-ui[pptx]`)

copyparty itself is bundled — no separate download needed. See [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) for attribution.

---

## Install

Install directly from the prebuilt wheel in [`dist/`](dist/):

```powershell
pip install dist\copyparty_ui-0.1.0-py3-none-any.whl
```

Or build it yourself:

```powershell
pip install build
python -m build --wheel
pip install dist\copyparty_ui-0.1.0-py3-none-any.whl
```

## Usage

```powershell
# Serve %USERPROFILE%\Downloads (default) on the default port
python -m copyparty_ui

# Serve a specific directory
python -m copyparty_ui --dir C:\files

# Serve an external drive on a custom port
python -m copyparty_ui --dir E:\ --port 8080

# Skip the startup file-hash scan — recommended for large drives (100GB+)
python -m copyparty_ui --dir E:\ --no-index
```

A console script is also installed: `copyparty-ui --dir E:\`.

### Options

| Flag | Default | Description |
|---|---|---|
| `--dir` | `%USERPROFILE%\Downloads` | Directory to serve |
| `-p`, `--port` | `3923` | copyparty backend port |
| `--ui-port` | `3924` | UI server port |
| `--no-browser` | off | Don't open a browser automatically on start |
| `--no-index` | off | Skip the startup file-hash scan and full-text content indexing (move/rename still work) |

Runtime state (content search index, file labels) is stored under `%LOCALAPPDATA%\copyparty_ui\`, separate from the served directory and the installed package.

---

## License

MIT for this project's own code. The bundled copyparty backend is MIT-licensed
by its original author — see [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).
