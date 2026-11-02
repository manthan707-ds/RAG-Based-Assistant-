<div align="center">

# 🔎 RAG Based Assistant

### Ask the course. Get the exact moment.

Ask a question about your lectures and jump straight to the video, at the second that answers it.

![HTML5](https://img.shields.io/badge/HTML5-single_file-e34f26?logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-vanilla-f7df1e?logo=javascript&logoColor=black)
![No build step](https://img.shields.io/badge/build-none-brightgreen)
![Deployed on Vercel](https://img.shields.io/badge/deploy-Vercel-black?logo=vercel)

**[Live demo](https://rag-based-assistant-psi.vercel.app/)

</div>

<!-- Add a screenshot: save it as docs/screenshot.png, then remove this comment markers
![RAG Based Assistant](docs/screenshot.png)
-->

---

## What is this?

**RAG Based Assistant** (Lecture Seek) is a bold, mobile-friendly web app for searching inside lecture videos and audio.
You ask a normal question, and instead of a wall of text it answers with **which lecture, which timestamp**, and opens the
player right there so you can start watching from that second.

This repository is the **complete front end**: one static page, no build step, no API keys.

## Features

**Ask and watch**
- Plain-language questions, answered with the lecture, the time (`V2 · 0:39`) and a video/audio player that opens at that second
- Replay button, suggested questions, and a clear "not found" reply that tells you which lectures still have nothing to search

**Your own lectures**
- **Add lecture:** upload `mp3`, `mp4`, `m4a`, `wav`, `webm`, `mov` or `mkv`, as a new lecture or attached to an existing one
- **Make it searchable** two ways:
  - **Transcribe (beta):** runs a small Whisper speech model *inside your browser* and indexes the whole lecture
  - **Add topics:** type one line per topic with its time, like `2:15 What a string is`
- **Uploads history:** newest first, with name, type, size and time. Play, re-add or delete any entry
- **Delete anything:** a file, a whole lecture, or all uploads, each with a tap-again confirmation

**Accounts screens**
- Sign in, Create account, Forgot password and a guest demo, with inline validation and a password strength meter

**Design**
- Very dark theme and a soft off-white light theme, bold type, hard borders and an electric accent
- Mobile first: 44px touch targets, 16px inputs (no iOS zoom), safe-area aware, keyboard and screen-reader friendly
- Respects `prefers-color-scheme` and `prefers-reduced-motion`

## How it works

1. **Search:** every lecture is split into timed clips. A question is tokenised, common words are dropped, and each clip
   is scored by how many of the question's words it covers, weighting rare words higher (IDF). The best clip above a minimum
   match wins.
2. **Player:** the winning clip's lecture file is opened with an `<audio>` or `<video>` element and seeked to the clip's start time.
3. **Getting text for new lectures:** a new file has no text until you add topics or run Transcribe, because a web page cannot
   read audio by itself. Until then it is searchable by title only.
4. **Storage:** files are kept in memory for the current tab (`blob:` URLs). The history list, topics and deletions are saved in
   `localStorage`, so after a refresh the list is still there and you re-add a file to play it.

> The demo ships with three sample lessons (HTML, CSS and JavaScript basics) so you can try it immediately.

## Run it locally

No install needed.

```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>

# any static server works
npx serve .
# or
python -m http.server 8000
```

Then open the address it prints (for example http://localhost:8000).
Opening `index.html` directly also works, but Transcribe needs `http://` or `https://`.

## Deploy

It is a static site, so any host works.

| Host | Steps |
|---|---|
| **Vercel** | New Project, import the repo, Framework **Other**, leave build and output empty, Deploy |
| **Netlify** | Drag the folder onto https://app.netlify.com/drop, or connect the repo |
| **Cloudflare Pages** | Create a Pages project and upload the folder or connect the repo |
| **GitHub Pages** | Settings, Pages, deploy from branch `main` / root |

`vercel.json`, `netlify.toml` and `_headers` add security headers (a Content-Security-Policy plus the usual hardening).
GitHub Pages ignores them and the site still works.

## Project structure

```
.
├── index.html     # the whole app: HTML, CSS and JavaScript
├── vercel.json    # security headers for Vercel
├── netlify.toml   # security headers for Netlify
├── _headers       # security headers for Cloudflare Pages / Netlify
└── README.md
```

## Privacy and security

- Your lecture files **never leave your browser**. There is no upload server.
- The only network requests are Google Fonts and, if you use Transcribe, the speech library from jsdelivr and the model
  files from Hugging Face (about 40 MB, cached by the browser after the first run).
- Pinned to `@huggingface/transformers@3.7.6`. The Content-Security-Policy only allows those hosts.
- Everything saved locally is under the keys `rba_uploads`, `rba_topics` and `rba_deleted`. Clear them any time from the Uploads panel
  or your browser settings.

## Current limitations

This is a front end demo, and it is honest about it:

- **Sign-in is simulated.** Any valid email and an 8+ character password works. Nothing is sent anywhere, and there is no Google sign-in yet.
- **Uploaded files are not stored permanently.** They live in the current tab, so re-add a file after a refresh to play it.
- **Transcribe is a beta.** It is slow on phones and very long videos, uses the small English model, and depends on your browser decoding the file.
- Search is keyword based, not semantic.

## Roadmap

- [ ] Backend (FastAPI): real accounts and sessions
- [ ] Upload endpoint with durable storage for lecture files
- [ ] Server-side Whisper transcription for any length of video
- [ ] Semantic search with embeddings (pgvector) and AI-written answers grounded in the transcript
- [ ] Multi-course library, shareable links to a timestamp
- [ ] Tests (Playwright) and CI

## Tech stack

HTML5, CSS custom properties (dark and light design tokens), vanilla JavaScript, the Web Audio API,
[Transformers.js](https://github.com/huggingface/transformers.js) with Whisper tiny (optional), Archivo and Geist fonts. Hosted on Vercel.

## Contributing

Issues and pull requests are welcome. For a big change, please open an issue first so we can talk it through.

## License

Add a `LICENSE` file to choose one (MIT is a common choice for projects like this).

## Author

Built by **Manthan Ghodkhande**.

If this helped you, a ⭐ on the repo is appreciated.
