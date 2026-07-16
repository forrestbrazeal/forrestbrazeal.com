# forrestbrazeal.com

The author site of Forrest Brazeal, built to promote his debut novel **_Paradox Inc._**
(Ballantine Books, Jan 27 2027).

A minimal, hand-built **static site** (plain HTML + CSS, no build step). Auto-deploys to
[Netlify](https://www.netlify.com/) on every push to `main`.

## Structure

```
index.html      # the whole site — one page, anchor-linked sections
styles.css      # all styling (eggshell theme, Montserrat + Lato, 3D book render)
images/         # book cover + headshot
netlify.toml    # publish config + headers (no build command)
```

## Editing

Everything lives in `index.html` and `styles.css`. Edit, commit, push — Netlify does the rest.

- **Add a News update:** copy one `<article class="news-item">` block in the `#news`
  section, edit the date/title/text, and put it at the top (newest first).
- **Swap the headshot:** replace `images/forrest-headshot.jpg` (used in About).
- **Contact form:** uses [Netlify Forms](https://docs.netlify.com/forms/setup/). Submissions
  appear in the Netlify dashboard under **Forms**; enable email notifications there.

To preview locally, run any static server, e.g.:

```
python3 -m http.server
```
