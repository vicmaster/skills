---
name: chrome-extension-creator
description: Use this skill when the user wants to create, build, or scaffold a Chrome browser extension from scratch. Triggers include requests like "create a Chrome extension", "build a browser extension", "make an extension that...", or any mention of Manifest V3, chrome.* APIs, content scripts, service workers, or extension popups. Generates a complete, installable extension with Manifest V3, working logic, icons, and installation instructions. Do NOT use for Firefox add-ons (different manifest), userscripts (Tampermonkey/Greasemonkey), or modifying existing extensions unless the user explicitly asks to rebuild.
---

# Chrome Extension Creator

Generates production-ready Chrome extensions using Manifest V3, fully functional and installable in under 2 minutes.

## Initial interaction

When invoked without a clear extension spec, ask the user one focused question:

> **What should your extension do?**
>
> Examples:
> - Pomodoro timer with notifications
> - Block distracting websites on a schedule
> - Extract emails/phones/links from any page
> - Dark mode for all websites
> - Track time spent per domain
> - Custom keyboard shortcuts for any site

If the user's request is already specific enough to build from, skip the question and proceed.

## Required clarifications before building

Before scaffolding, confirm or infer:

1. **Trigger surface**: popup, content script, background service worker, options page, side panel, or new tab override
2. **Permissions needed**: only request what's actually used (`activeTab` over `tabs` when possible, no `<all_urls>` unless required)
3. **Storage needs**: `chrome.storage.local` (default), `chrome.storage.sync` (cross-device, 100KB limit), or none
4. **Host permissions**: specific domains vs. all sites — default to specific

State assumptions inline rather than asking multiple questions. One round of clarification max.

## File structure to generate

```
extension-name/
├── manifest.json          # Manifest V3, minimum permissions
├── popup.html             # If popup is used
├── popup.js               # Popup logic, no inline scripts (CSP)
├── popup.css              # Scoped styles
├── background.js          # Service worker (not persistent background page)
├── content.js             # If page interaction needed
├── icons/
│   ├── icon16.png
│   ├── icon48.png
│   └── icon128.png
└── README.md              # Install + usage instructions
```

Omit files that aren't needed. Don't generate empty `content.js` if there's no content script.

## Manifest V3 requirements (non-negotiable)

- `"manifest_version": 3`
- Background = service worker, not persistent page: `"background": { "service_worker": "background.js" }`
- No remote code execution, no `eval`, no inline `<script>` in HTML
- Action API: `"action"` not `"browser_action"` or `"page_action"`
- Host permissions in `"host_permissions"`, separate from `"permissions"`
- Use `chrome.scripting.executeScript` instead of `chrome.tabs.executeScript`

## Code quality rules

- **No half-finished code.** Every function the user can trigger must work end-to-end. No `// TODO: implement` stubs.
- **No external dependencies by default.** Vanilla JS unless the user requests a framework. If a framework is needed, bundle it locally — no CDN imports (CSP will block them).
- **Async/await over callbacks.** Modern `chrome.*` APIs return promises in MV3.
- **Defensive messaging.** Always check `chrome.runtime.lastError` after API calls that can fail.
- **Storage writes are batched.** Don't call `chrome.storage.set` in a loop.

## Icon generation

Generate three PNG icons (16x16, 48x48, 128x128) using Python with Pillow. Keep the design simple, single-concept, high-contrast — it has to read at 16px. If Pillow is unavailable, generate SVG and convert with ImageMagick or `cairosvg`. Save to `icons/` in the extension folder.

## Popup design (when applicable)

- Fixed width 320–400px, height grows to content (max 600px before Chrome scrolls)
- System font stack, not web fonts (CSP + load time)
- Dark mode via `prefers-color-scheme`
- All interactive elements keyboard-accessible

## README contents

The generated README must include:

1. One-paragraph description of what the extension does
2. Installation steps (loading unpacked):
   - Open `chrome://extensions/`
   - Enable **Developer mode** (top right)
   - Click **Load unpacked**
   - Select the extension folder
3. Usage instructions per feature
4. Permissions explanation — what each one is for and why
5. Known limitations

## Output delivery

After generating, present the folder to the user so they can download it. Then give a 2-3 sentence summary of what was built and how to install — don't restage the README inline.

## Common pitfalls to avoid

- Requesting `tabs` permission when `activeTab` would work (causes scary install warning)
- Inline event handlers in HTML (`onclick="..."`) — blocked by CSP
- Trying to `import` ES modules in service workers without `"type": "module"` in manifest
- Using `localStorage` in service workers — it doesn't exist there; use `chrome.storage`
- Forgetting that service workers are killed after ~30s idle — persist state to storage, don't keep it in memory
- Loading remote scripts or styles — blocked in MV3
