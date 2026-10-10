# How to Edit Your Personal Webpage

Your whole site is one file, `index.html`, plus your photo `Protik.jpg`. This guide shows how to change the text, add new items, change the look, and put the changes online.

**Your site:** https://paul-protik.github.io
**Your repository:** https://github.com/paul-protik/paul-protik.github.io

---

## 1. The basic workflow

1. **Open** `index.html` in a text editor. [VS Code](https://code.visualstudio.com) is free and recommended. Notepad also works.
2. **Change** the text or style (see sections below).
3. **Save** the file.
4. **Preview:** double-click `index.html` to open it in your browser. After each change, press **Ctrl+R** (Mac: **Cmd+R**) to refresh.
5. **Publish** when it looks right (see section 8).

> Tip: Keep a backup copy of the last working `index.html` before big changes. If something breaks, press **Ctrl+Z** to undo or restore the backup.

---

## 2. How the file is organised

Use **Ctrl+F** to find things quickly.

| Part of the file | What it controls | Search for |
|---|---|---|
| `<style> ... </style>` | Colours, fonts, sizes, spacing | `:root` |
| `<nav>` | The menu links at the top | `<nav` |
| Hero section | Your name, role line, photo | `class="hero"` |
| Research | The research paragraphs | `id="research"` |
| Publications | Your papers | `id="publications"` |
| Talks | Your talks | `id="talks"` |
| Background | Jobs, education, awards | `id="background"` |
| Contact | Email and links | `id="contact"` |
| Footer | The © line at the bottom | `<footer>` |

HTML uses **tags** that come in pairs, such as `<p>text</p>`. Only change the text **between** the tags and leave the tags themselves alone.

---

## 3. Editing text

Find the sentence you want to change and edit it. For example, in the Research section:

```html
<p>My research covers secure multiparty computation (MPC), ...</p>
```

Change the words between `<p>` and `</p>`.

**Special characters**

| To show | Type |
|---|---|
| `&` | `&amp;` (for example `S&amp;P`) |
| `<` | `&lt;` |
| Bold text | `<b>text</b>` |
| Italic text | `<i>text</i>` |
| A line break | `<br>` |
| A link | `<a href="https://example.com">link text</a>` |

---

## 4. Adding new items

Each item in a list is one `<li> ... </li>` block. To add one, **copy a whole block**, paste it where you want it, and change the text. Newer items go at the **top** of the list.

### Add a publication

Copy this block into the `<ul class="list">` inside `id="publications"`:

```html
<li>
  <span class="when">2027</span>
  <div>
    <h3>Paper title here</h3>
    <p>A. Author, <b>P. Paul</b>, B. Author.<br>
    <span class="venue v-sp">IEEE Symposium on Security and Privacy (S&amp;P)</span>
    <span class="tag">(Core A*)</span><br>
    <a href="https://eprint.iacr.org/2027/0000.pdf">ePrint</a></p>
  </div>
</li>
```

- **Venue colours:** use `v-sp` (blue) for S&P, `v-asia` (purple) for ASIACRYPT, and `v-pets` (green) for PoPETS. For a new venue, pick one of these or add a new colour (see section 6).
- **Under submission:** replace the venue lines with `<span class="tag">Under submission</span>`.
- **No ePrint link yet:** delete the `<br><a href=...>ePrint</a>` part.

### Add a talk

Copy this into the list inside `id="talks"`:

```html
<li><span class="when">Month 2027</span><div><h3>Talk title</h3><p>Event name, City, Country</p></div></li>
```

### Add a job, degree, or award

Copy this into the list inside `id="background"`:

```html
<li><span class="when">2027 – now</span><div><h3>Position or degree</h3><p>Institution, Country. Extra details.</p></div></li>
```

### Add a new link in Contact

Add one line inside `<div class="links">`:

```html
<a href="https://www.linkedin.com/in/yourname">LinkedIn</a>
```

### Add a new menu item at the top

Add a link inside `<nav>` that matches a section `id`. For example, if you create a section with `id="news"`, add `<a href="#news">News</a>`.

---

## 5. Changing the photo

- **Replace the photo:** put the new image in the same folder as `index.html`, with the same filename (`Protik.jpg`). Or change the filename in the `<img src="Protik.jpg" ...>` line.
- **Keep it small:** resize the photo to about 600×600 pixels (use [squoosh.app](https://squoosh.app)). A smaller file makes the page load faster, especially on phones.
- **Change the size:** find `.profile-pic` in the style block and change `width` and `height`. Keep them equal so it stays a circle.

```css
.profile-pic { width:240px; height:240px; ... }
```

- **Change the crop:** edit `object-position:50% 35%`. The second number moves the visible area up (lower) or down (higher).
- **Change the shape:** `border-radius:50%` is a circle. Use `12px` for a rounded square.
- **Phones have their own size:** look for `@media (max-width:40rem)` just below.

---

## 6. Changing colours

All colours are defined once, at the very top of the style block:

```css
:root {
  --bg:#e6edf1;      /* page background */
  --ink:#17232e;     /* main text */
  --muted:#4d5f6d;   /* dates and grey text */
  --accent:#f0b429;  /* yellow highlight under your name */
  --teal:#1d5a63;    /* links */
  --line:#b9c8d1;    /* thin divider lines */
  --c-sp:#1f5fa8;    /* S&P venue colour */
  --c-asia:#8a3f9e;  /* ASIACRYPT venue colour */
  --c-pets:#2f7a3a;  /* PoPETS venue colour */
}
```

Replace a hex code (like `#f0b429`) with any other. Find codes at [coolors.co](https://coolors.co).

**Dark mode has its own set.** Just below, inside `@media (prefers-color-scheme: dark)`, the same names are defined again. When you change a colour, change it in **both** places. Test dark mode by switching your computer's theme.

**Adding a colour for a new venue**

1. Add two lines in `:root` (light) and in the dark block, such as `--c-ccs:#b5471f;` (light) and `--c-ccs:#f0a07c;` (dark).
2. Add a class below the other venue classes: `.v-ccs { color:var(--c-ccs); }`.
3. Use it in a paper: `<span class="venue v-ccs">ACM CCS</span>`.

---

## 7. Changing fonts

Changing a font takes two steps.

**Step A: choose a font** at [fonts.google.com](https://fonts.google.com). Note the name and the weights you want (for example Lora, 600 and 800).

**Step B: add it to the file.**

1. In the `<link href="https://fonts.googleapis.com/css2?family=...">` line near the top, add `&family=Lora:wght@600;800` before `&display=swap`.
2. Use it in the CSS:
   - **Your name:** in `.hero-content h1`, change `font-family:"Fraunces"` to `font-family:"Lora"`.
   - **All other text:** in `body {`, change `font-family:"Bricolage Grotesque"`.

Always keep a fallback after the name, like `"Lora", Georgia, serif`, in case the font fails to load.

**Font size**

- Name size: in `.hero-content h1`, edit `font-size:clamp(2.75rem, 10vw, 5.25rem)`. The first and last numbers are the minimum and maximum sizes.
- Body text size: in `body {`, edit `font-size:1.0625rem`.
- Section headings: in `h2 {`, edit `font-size:1.75rem`.

---

## 8. Publishing your changes

### Option A: In the browser (no Git needed)

1. Go to your repository on GitHub.
2. Click **Add file → Upload files** and drag in the new `index.html` (and `Protik.jpg` if you changed it).
3. Click **Commit changes**.

### Option B: With Git (from your computer)

In the folder that contains your site, run:

```bash
git add index.html Protik.jpg
git commit -m "Update website"
git push
```

If you didn't change the photo, you can leave out `Protik.jpg`.

Your site refreshes within **one to two minutes**. If you don't see the changes, do a hard refresh (**Ctrl+Shift+R**). You can check progress in the **Actions** tab of your repository: a green tick means it's live.

---

## 9. Common problems

| Problem | Fix |
|---|---|
| The page looks broken after an edit | You probably deleted or added a `<` or `>` by accident. Press **Ctrl+Z**, or restore your backup. |
| A section is missing | Check that every `<li>` has a matching `</li>` and every `<div>` has a matching `</div>`. |
| The photo doesn't show | The filename must match exactly, including capital letters (`Protik.jpg`), and the file must be in the same folder as `index.html`. |
| The font didn't change | Check that the font is added to the Google Fonts `<link>` and spelled correctly in the CSS. |
| The site didn't update | Wait two minutes, hard refresh (**Ctrl+Shift+R**), and check the **Actions** tab on GitHub. |
| `&` shows strangely | Write `&amp;` instead of `&` in the text. |

---

## 10. Quick checklist before publishing

- [ ] Names, dates and affiliations are correct
- [ ] All links open the right pages (click each one in your preview)
- [ ] The page looks right on a phone (press **F12** in Chrome, then click the phone icon)
- [ ] Both light mode and dark mode look fine
- [ ] The photo file is small (under about 200 KB)
