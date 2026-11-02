# RAG Based Assistant (site)

One static page: `index.html`. No build step, no server, no keys.

## Deploy in about 2 minutes (pick one)

**Netlify (easiest):** unzip, open https://app.netlify.com/drop and drop this folder. Done.

**Vercel:** push this folder to a GitHub repo, then Vercel > Add New > Project > pick the repo > Deploy
(Framework preset: Other, no build command, output directory `.`). Or run `npx vercel --prod` inside the folder.

**Cloudflare Pages:** Workers & Pages > Create > Pages > Upload assets > drop this folder.

**GitHub Pages:** push the folder to a repo, Settings > Pages > Deploy from branch > `main` / root.
(GitHub Pages ignores `_headers`, `netlify.toml` and `vercel.json`; the site still works.)

`_headers`, `netlify.toml` and `vercel.json` add security headers (a Content-Security-Policy that allows only
this page, Google Fonts and in-browser media).

## What this site is (and is not)

It is the finished front end: sign in / create account screens, the chat that points to the video and the
second, Add lecture, the Uploads list and the delete options, with dark and light themes, phone friendly.

It does **not** have a backend yet, so:
- sign-in is simulated (any valid email and an 8+ character password works; nothing is sent anywhere),
- answers come from three built-in sample lessons plus the lectures you add in the same browser,
- uploaded files stay in the visitor's browser tab and are gone after a refresh (only the history list is kept).

For real accounts, real storage and real course search, connect it to the FastAPI backend in
`rag-based-assistant.zip`.
# RAG-Based-Assistant-
