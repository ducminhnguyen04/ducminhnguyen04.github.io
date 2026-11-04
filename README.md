# Duc Minh Nguyen — academic website

Static site (`index.html` + `style.css`), no build step. The CV in `cv/` is local only (git-ignored, not published).

```
index.html        the whole page
style.css         styles
assets/           photo, thumbnails, GIF/mp4 demos
cv/cv.tex         CV source  ->  cd cv && latexmk -pdf cv.tex  ->  cv/cv.pdf
```

## Deploy to GitHub Pages (once)

1. On GitHub, account `ducminhnguyen04`: create a **public** repo named exactly `ducminhnguyen04.github.io` (empty, no README).
2. In this folder:
   ```bash
   git init -b main
   git add .
   git commit -m "Initial website"
   git remote add origin https://github.com/ducminhnguyen04/ducminhnguyen04.github.io.git
   git push -u origin main
   ```
3. Repo → Settings → Pages → Source: "Deploy from a branch", Branch: `main` / `(root)`.
4. After 1–2 minutes the site is live at https://ducminhnguyen04.github.io.
5. (Optional) Google Search Console → add the URL property → request indexing so Google finds your name sooner.

`.gitignore` keeps `cv/`, `NguyenMinhDuc_CV.pdf`, `Sim2Real.pdf` and `assets/avatar.JPG` out of the repo.

## Update content

After any change: `git add . && git commit -m "..." && git push`. The site updates in about a minute.

- **Photo:** put `assets/profile.jpg` (square, ~400×400) and change `src="assets/profile.svg"` in `index.html`.
- **New paper:** copy one `<div class="item">…</div>` block in the Publications section, edit title/authors/venue/links,
  and add a line to News. Add the same paper to `cv/cv.tex` (copy a `\pub{...}` block) and rebuild the CV locally.
- **Thumbnail / demo** (inside `<div class="media">`, pick one):
  - image or GIF: `<img src="assets/foca.gif" alt="FOCA demo" loading="lazy">`
  - mp4 in repo (plays muted when scrolled into view):
    `<video src="assets/foca.mp4" muted loop playsinline preload="none" data-autoplay></video>`
  - YouTube (loads only when scrolled into view, muted):
    `<div class="yt" data-id="YOUTUBE_ID" data-title="FOCA demo"></div>`

  Keep files small: mp4 under ~5 MB (e.g. `ffmpeg -i in.mp4 -vf scale=640:-2 -an -crf 28 out.mp4`); prefer mp4 over large GIFs.
- **CV:** edit `cv/cv.tex`, run `cd cv && latexmk -pdf cv.tex` (local only, not pushed).
