# Hanske De Schaker — website

This folder **is** the website hanskedeschaker.eu. It's plain files: no Squarespace,
no database, nothing to install or "build". Every page is one HTML file you can open
and edit in VS Code.

## What's in the folder

| File / folder | What it is |
|---|---|
| `index.html` | Start page |
| `evenementen.html` | Evenementen |
| `kalender.html` | Kalender (with the filter buttons) |
| `geschiedenis.html` | Geschiedenis and the list of clubkampioenen |
| `contact.html` | Contact and the lessenreeks |
| `start.html` | Sends old links (…/start) to the homepage. Keep it. |
| `css/style.css` | All colours, fonts and layout, for every page |
| `fonts/` | The two typefaces. Stored here, so no outside service is needed. |
| `images/` | Photos, one folder per page, plus the logo |
| `favicon.svg`, `apple-touch-icon.png` | The little icon in browser tabs and on phones |
| `.nojekyll` | Tells GitHub Pages to publish the files exactly as they are. Keep it. |

## See the site on your computer

1. In VS Code, install the extension **Live Server** (by Ritwick Dey):
   open the Extensions panel (`Ctrl+Shift+X`), search "Live Server", click Install.
2. **File → Open Folder…** and pick this folder.
3. Right-click `index.html` → **Open with Live Server**.
   The site opens in your browser, and refreshes by itself every time you save (`Ctrl+S`).

(Double-clicking `index.html` also works, it just doesn't refresh by itself.)

## Common changes

### Change some text
Open the page's `.html` file, find the sentence with `Ctrl+F`, change it, save.
Text sits between tags, like `<p>…</p>` (a paragraph) or `<h3>…</h3>` (a heading).
Change only the words between the tags.

### Add an event (Evenementen)
1. Prepare the photos (see *Adding photos* below) and put them in `images/evenementen/`.
2. In `evenementen.html`, copy a whole `<article class="event"> … </article>` block and
   paste it at the top of the right year (newest first).
3. Change the title, date, text and photo file names.

```html
<article class="event">
  <h3>Titel van het evenement</h3>
  <p class="date">Vrijdag 03/09/2027</p>
  <p>Tekst…</p>
  <div class="photos">
    <img src="images/evenementen/2027-voorbeeld-1.webp" width="1600" height="1200" alt="Titel van het evenement, foto 1" loading="lazy" decoding="async">
  </div>
</article>
```

For a **new year**, copy a whole `<section class="year"> … </section>` block and change
the year in all three places (`aria-labelledby="jaar-2027"`, `id="jaar-2027"` and the visible `2027`).

### Adding photos
- **Make them smaller first.** Phone photos are 3–6 MB; about 200 KB is plenty on a website.
  Easiest free tool: [squoosh.app](https://squoosh.app). Open the photo, choose **WebP**,
  tick **Resize** and set the width to 1600, then download.
- Use simple names: lowercase, no spaces, e.g. `2027-nieuwjaar-1.webp`.
- `width` and `height` in the `<img>` tag are the photo's size in pixels (Squoosh shows them).
  They let the page keep space free while the photo loads. If they're slightly off, nothing breaks.
- `alt` is a short description, read aloud to blind visitors and used by search engines.

### Update the calendar
In `kalender.html`, every evening is one block:

```html
<li class="event-row" data-category="club">
  <time datetime="2027-09-03">03</time>
  <span class="what"><strong>Club Ronde 1-1</strong> <span class="tag">Clubkampioenschap</span></span>
</li>
```

- `data-category` is `club`, `ovic`, `rapid` or `event` (= "Andere"). It sets the coloured
  square and which filter button shows the evening.
- `datetime` is the full date (year-month-day); the number shown is the day.
- No label? Leave out `<span class="tag">…</span>`.
- A special evening? Use `class="event-row highlight"`.
- Each month is a `<section class="month">` with its name in the `<h2>`.
  For a new season, copy a month block and change the name and the evenings.

### Add a club champion
At the end of the list in `geschiedenis.html`:

```html
<li><span class="year-number">2027</span> <span>Naam</span></li>
```

### Change colours or fonts
Everything is at the top of `css/style.css`, in the `:root` block.
For example, `--red: #a3302b;` is the brick red used in the menu, the years and the footer.

### The menu
The menu and the footer are repeated in each of the 5 pages. If you rename or add a page,
change the menu in all 5 files. VS Code's **Find in Files** (`Ctrl+Shift+H`) does it in one go.

## Publishing changes

The site is hosted for free on GitHub Pages. After editing:

- **Easiest:** on github.com, open the repository → **Add file → Upload files** → drag in the
  files you changed (same folders as here) → **Commit changes**. The live site updates within a minute or two.
- **Later, once you're comfortable:** VS Code's Source Control panel can do this in one click (Commit, then Sync).

GitHub adds a file called `CNAME` to the repository when you connect the domain.
**Don't delete it**: it's what links hanskedeschaker.eu to the site.

## How the domain is connected (for reference)

hanskedeschaker.eu is registered at Squarespace Domains. Its DNS records point to GitHub Pages:

| Type | Host | Value |
|---|---|---|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| CNAME | www | *your-github-username*.github.io |

Keep the domain's auto-renew switched on at Squarespace, or move the domain to another registrar later.

## Credits

Fonts: Abril Fatface (TypeTogether) and Libre Franklin (Impallari Type), both under the
SIL Open Font License. The licences are in `fonts/`.
