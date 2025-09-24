# Puter.js Full-Feature Demo

A single-page, frontend-only web application that demonstrates the complete Puter.js SDK across AI, Cloud Storage (FS), Key-Value Store (KV), Hosting, Auth, Networking, Workers, UI, Utils, Drivers, and Permissions APIs.

This app requires no backend and no API keys. It loads `https://js.puter.com/v2/` and runs entirely in the browser.

---

## Table of Contents

- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
- [Feature Matrix](#feature-matrix)
- [How to Use](#how-to-use)
  - [AI](#ai)
  - [Auth](#auth)
  - [Cloud Storage (FS)](#cloud-storage-fs)
  - [Hosting](#hosting)
  - [Apps API](#apps-api)
  - [Key-Value Store (KV)](#key-value-store-kv)
  - [Networking](#networking)
  - [Workers](#workers)
  - [UI](#ui)
  - [Utils](#utils)
  - [Drivers](#drivers)
  - [Permissions (Privileged)](#permissions-privileged)
- [Notes & Best Practices](#notes--best-practices)
- [Troubleshooting](#troubleshooting)
- [Security & Privacy](#security--privacy)
- [Credits](#credits)
- [License](#license)

---

## Overview

This project is meant as a reference implementation and a quick playground for Puter.js. Each card in `index.html` provides runnable examples of one or more APIs, including optional/advanced parameters.

---

## Prerequisites

- A modern browser with internet access
- Optional: A Puter account (you will be prompted to sign in when a cloud feature is used)

---

## Getting Started

1. Open `index.html` directly in your browser, or serve statically with any HTTP server.
2. Interact with the on-page sections to execute demos.
3. For first-time cloud access, Puter.js will show a sign-in flow automatically.

> Tip: A simple dev server example: `python -m http.server 8000` then visit `http://localhost:8000/`.

---

## Feature Matrix

The following SDK areas from the requirement are implemented and demoed:

- AI: `chat` (string/messages/image/tools/stream), `img2txt`, `txt2img` (model/quality + image-to-image), `txt2speech` (language/voice/engine)
- Auth: `signIn`, `signIn({ attempt_temp_user_creation })`, `signOut`, `isSignedIn`, `getUser`
- FS: `write`, `read`, `read({ offset, byte_count })`, `mkdir`, `readdir`, `rename`, `copy`, `move`, `delete`, `stat`, `getReadURL`, `upload`, `space`
- Hosting: `create`, `update`, `delete`, `get`, `list`
- Apps: `create`, `list`, `get`, `update`, `delete`
- KV: `set`, `get`, `list()`, `list(pattern)`, `list(true)`, `incr`, `decr`, `del`, `flush`
- Networking: `net.fetch` (GET/POST), `net.Socket`, `net.tls.TLSSocket`
- Workers: `create` (deploy), `exec`, `list`, `get`, `delete` (router used in deployment)
- UI: `alert`, `prompt`, `authenticateWithPuter`, `createWindow`, `showSpinner`/`hideSpinner`, `contextMenu`, `setMenubar`, pickers (`showOpenFilePicker`, `showSaveFilePicker`, `showDirectoryPicker`, `showColorPicker`, `showFontPicker`), `getLanguage`, `launchApp`, `parentApp`, `on` (localeChanged/themeChanged), `onWindowClose`, `onLaunchedWithItems`, `onItemsOpened`, `wasLaunchedWithItems`, `setWindowTitle/Size/Position/Width/Height/X/Y`, `exit`
- Utils: `env`, `appID`, `randName`, `print`
- Drivers: `drivers.call` (illustrative)
- Permissions: `grantApp`, `revokeApp`, `grantAppAnyUser`, `revokeAppAnyUser`, `grantOrigin`, `revokeOrigin`, `grantGroup`, `revokeGroup`, `grantUser`, `revokeUser` (guarded/privileged)

---

## How to Use

### AI
- Chat: basic string prompt; streaming toggle; messages[] mode; image URL context; function-calling tools.
- Image to Text: paste an image URL to extract text.
- Text to Image: prompt → image, with `model`/`quality` options; plus image-to-image using `input_image` and `input_image_mime_type`.
- Text to Speech: choose language, voice, and engine; audio plays in-page.

### Auth
- Test sign in/out. `isSignedIn()` displays status. `getUser()` prints the current user.
- A quick action to test `attempt_temp_user_creation` is provided.

### Cloud Storage (FS)
- Write and read files, including partial reads via `offset` and `byte_count`.
- Create directories (with parent creation), list directories, rename/move/copy/delete items, `stat` files, generate temporary read URLs, upload files, and inspect user `space`.

### Hosting
- Create and host a demo website directory with a random subdomain.
- Update the hosted directory, delete, get details, and list all subdomains.

### Apps API
- Create, list, get, update, and delete apps by name.

### Key-Value Store (KV)
- `set`, `get`, `list` (keys only or including values), `incr`, `decr`, `del`, `flush`.
- Pattern-based listing with wildcards is included.

### Networking
- `net.fetch` GET and POST with headers/body.
- Raw `Socket` (TCP) and `TLSSocket` examples print response text to the output panel.

### Workers
- Deploy a tiny worker with a `/api/hello` route and then call it.
- List, get, and delete workers.
- Note: allow 5–30 seconds for edge propagation after deployment/updates.

### UI
- Dialogs (alert/prompt), spinners, new windows, context menus, menubars, social sharing, and pickers.
- Language and theme broadcasts via `puter.ui.on(...)`.
- Parent/child `AppConnection` demo: listens to messages when launched as a child.
- Window management helpers to update title/size/position.

### Utils
- Display `env` and `appID`, generate a `randName`, and demonstrate `puter.print`.

### Drivers
- Illustrative form for `puter.drivers.call(interface, driver, method, args)`; may require privileges depending on target.

### Permissions (Privileged)
- Grant or revoke permissions for App, AnyUser, Origin, Group, and User.
- Most operations require privileged contexts; the UI will show a helpful error if not available.

---

## Notes & Best Practices

- Some operations (e.g., Workers deploy, Hosting) require propagation time across edge servers before results are visible.
- When demonstrating potentially privileged APIs (Drivers/Perms), the UI captures and displays errors cleanly.
- For KV, prefer scoped prefixes for production apps to avoid key collisions.
- For long-running AI responses, use streaming for better UX.

---

## Troubleshooting

- Nothing happens on cloud actions: ensure you are signed in via the Auth section or let Puter.js prompt you automatically.
- Worker test fails immediately after deploy: wait 5–30 seconds and try again (edge propagation).
- Socket/TLS demos not printing: check network access policies and browser console.
- Privilege errors in Drivers/Perms: these APIs require privileged contexts; behavior is environment-dependent.

---

## Security & Privacy

Puter.js handles authentication and authorization, and apps are sandboxed by default (app data is under `~/AppData/<app-id>/`). Users cover their own usage costs (User Pays Model). Review Puter’s privacy stance and policies for details.

---

## Credits

- Powered by [Puter](https://developer.puter.com)
- Footer includes the required link: “Powered by Puter”

---

## License

This project is provided for demonstration purposes. Verify licensing, terms, and acceptable use with the Puter platform before deploying to production.
