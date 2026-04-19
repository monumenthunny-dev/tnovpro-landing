# TNovPRO

**B2B messenger and collaboration platform for [PM Nova](https://pm-nova.ru) — an engineering / construction company.**

> Internal corporate tool used by ~70 employees for daily work communication, project coordination, and voice calls. Hosted on private infrastructure at `tnov.pm-nova.ru` (accessible only from the company network / corporate VPN).

---

## Features

- **Telegram-style chat**: direct and group chats, message grouping, replies (swipe on mobile, hotkey `R` on desktop), reactions, context menu, search, forwards, @mentions, markdown, spoilers, scheduled messages.
- **Voice & video calls**: WebRTC via LiveKit — 1-to-1 and group conferences, screen sharing.
- **Stickers**: 700+ across 12 categories (smileys, hearts, gestures, animals, food, sports, nature, transport, objects, symbols, celebrate, flags) — rendered as large Twemoji SVG without bubble background.
- **GIF search via [GIPHY](https://giphy.com)** — in-app picker with trending and search, integrated in the chat input. *Powered by GIPHY* attribution displayed in the picker footer per attribution guidelines.
- **Custom chat backgrounds**: 21 gradient / solid presets plus user-uploaded images, per-user per-chat, with an "apply to peer" suggestion flow for direct chats.
- **6 accent color themes** (emerald, blue, purple, rose, amber, teal) that work in both light and dark modes.
- **Typing indicator** in chat list previews with safety auto-clear, file attachments, voice messages, message editing, multi-select deletion.
- **Productivity modules**: surveys / polls, requests / tickets, kanban projects, news feed, timesheets.
- **Desktop notifier** (Electron tray app) delivering native system notifications for new messages.

## GIPHY Integration

GIF search is wired through a server-side proxy that keeps the API key private. Endpoints `/api/gif/trending` and `/api/gif/search` normalize Giphy responses and cache popular results (30 minutes for trending, 10 minutes per search query) to stay well under rate limits.

The in-app GIF picker:
1. Opens from the chat composer alongside emoji and sticker buttons.
2. Shows a search field (debounced as the user types) and a grid of trending or searched GIFs.
3. Has a **Powered by GIPHY** attribution link in the footer.

Selecting a GIF sends it as an attachment in the current chat.

## Stack

- **Frontend**: React 18, Vite, Tailwind CSS, Framer Motion, Zustand, Socket.IO client, LiveKit Components.
- **Backend**: Node.js 20, Express, PostgreSQL, Socket.IO, LiveKit server SDK, Helmet, DOMPurify, JWT auth.
- **Mobile**: React Native client, Android APK build via GitHub Actions.
- **Infrastructure**: Docker Compose (frontend / backend / postgres / livekit), nginx reverse proxy with SSL termination, split-horizon DNS for internal vs external access.

## Status

Active development. Production deployment at `tnov.pm-nova.ru` (corporate-only access). Staging at `stg.tnov.pm-nova.ru`. The source repository is private by company policy; this page exists as a public overview of the product.

For questions, contact the engineering team at PM Nova: [https://pm-nova.ru](https://pm-nova.ru).