# Jing Su — Portfolio Site

A single-page portfolio. No build step, no npm, no framework. Two files do the work:

```
index.html          the entire site — HTML, CSS, and JS in one file
Jing_Su_Resume.pdf  linked from the "Download résumé" buttons
.nojekyll           tells GitHub Pages to serve files as-is
README.md           this file
```

To preview it before publishing, just double-click `index.html`. It opens in your browser and works offline (fonts need a connection, but the layout holds without them).

---

## Publish it — Option A: no command line

Fastest path. About five minutes.

1. Go to **github.com/new**. Name the repository exactly:

   ```
   YOUR-USERNAME.github.io
   ```

   Replace `YOUR-USERNAME` with your GitHub username, lowercase. Set it to **Public**. Don't add a README — you already have one. Click **Create repository**.

2. On the empty repo page, click **uploading an existing file**.

3. Drag in all four files: `index.html`, `Jing_Su_Resume.pdf`, `.nojekyll`, `README.md`.

   > If `.nojekyll` doesn't appear when you drag — it's a hidden file. On macOS press `Cmd + Shift + .` in Finder to show hidden files; on Windows, enable "Hidden items" in File Explorer's View tab.

4. Click **Commit changes**.

5. Go to **Settings → Pages**. Under "Build and deployment", set Source to **Deploy from a branch**, branch **main**, folder **/ (root)**. Save.

6. Wait 1–2 minutes. Your site is live at:

   ```
   https://YOUR-USERNAME.github.io
   ```

Using the `USERNAME.github.io` name gives you the clean root URL. If you name the repo something else — say `portfolio` — the site lives at `https://YOUR-USERNAME.github.io/portfolio/` instead. Everything still works; the links are all relative.

---

## Publish it — Option B: command line

```bash
cd path/to/portfolio

git init
git add .
git commit -m "Portfolio site"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/YOUR-USERNAME.github.io.git
git push -u origin main
```

Then do step 5 above (Settings → Pages) once. After that, every update is three commands:

```bash
git add .
git commit -m "Update work section"
git push
```

Changes go live about a minute after each push.

---

## Custom domain (optional)

If you buy a domain like `jingsu.dev`:

1. Create a file named `CNAME` in the repo root containing one line — your domain, nothing else:

   ```
   jingsu.dev
   ```

2. At your domain registrar, add these DNS records:

   | Type  | Name | Value |
   |-------|------|-------|
   | A     | @    | 185.199.108.153 |
   | A     | @    | 185.199.109.153 |
   | A     | @    | 185.199.110.153 |
   | A     | @    | 185.199.111.153 |
   | CNAME | www  | YOUR-USERNAME.github.io |

3. In **Settings → Pages**, enter the domain and check **Enforce HTTPS** once the certificate is issued (can take up to an hour).

---

## Editing the content

Open `index.html` in any text editor. It's organized top to bottom with comment banners, so search for these to jump around:

| Search for | What it controls |
|---|---|
| `TOKENS` | All colors and fonts, in one place at the top |
| `SIGNATURE ELEMENT` | The hero pipeline with the counting numbers |
| `SELECTED WORK` | Production project cards |
| `ARCHITECTURE BUILDS` | Graduate project cards |
| `CAPABILITIES` | The evidence matrix |
| `BACKGROUND` | Experience timeline and education |

### Change the colors

Edit the values under `:root` at the top of the `<style>` block. The accent appears in exactly two variables:

```css
--amber: #FFB454;   /* metrics, status, primary buttons */
--peri:  #9FB3FF;   /* secondary labels and hover states */
```

Swap those two and the whole page shifts. Nothing else needs touching.

### Add a project card

Copy an existing `<article class="card reveal">` block and edit the text. The status chip is one of three:

```html
<span class="chip chip-prod">In production</span>     <!-- amber -->
<span class="chip chip-prog">In progress</span>       <!-- periwinkle -->
<span class="chip chip-build">Hands-on build</span>   <!-- grey -->
```

### Change a number in the hero pipeline

The animation reads the target from the attribute, so edit that — not the text between the tags:

```html
<div class="stage-num" data-count="25733">0</div>
```

### Update the résumé

Replace `Jing_Su_Resume.pdf` with a new file **using the same filename**, and both download buttons keep working. If you rename it, update the two `href="Jing_Su_Resume.pdf"` links.

---

## Before you publish — four things to check

1. **The evidence dots.** In the Capabilities section I assigned each item a level (production / hands-on build / working knowledge) by reading your resume and career document. Some were judgment calls — Lambda, Step Functions, CloudWatch, and Redis especially. Skim that section and move any dot you'd defend differently in an interview, because that's exactly where it will get tested.

2. **Your GitHub link.** There isn't one on the site. If you have a public repo worth showing, add a button next to the LinkedIn one in the hero and contact sections.

3. **Your phone number.** Deliberately left off. Published on a public page it collects recruiter spam and robocalls, and the résumé PDF already carries it for anyone who's serious. Add it to the contact section if you'd rather have it there.

4. **Flowmerce AI wording.** That card says milestone one is delivered and forecasting is in progress, with the rest framed as roadmap. Worth re-reading against where the project actually stands the week you publish.
