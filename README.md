# GAIEA Lab Website

The GAIEA Lab website: a Jekyll site deployed to GitHub Pages by GitHub Actions. It is adapted from the
[Beery Lab site](https://github.com/mitbeerylab/mitbeerylab.github.io), which was itself adapted from the
[Coley Group site](https://github.com/coleygroup/coleygroup.github.io).

## Where things live

| What | File(s) | Updated by |
| --- | --- | --- |
| Lab name, logo, links, institution | `_config.yml` | hand |
| Home page text | `_pages/home.md` | hand |
| Join Us page | `_pages/positions.md` | hand |
| News (four newest on home page) | `_data/news.yml` | hand |
| People | `_data/pi.yml`, `postdocs.yml`, `grad_students.yml`, `msvisit.yml`, `undergrads.yml`, `alumni.yml`; photos in `images/teampic/` | hand |
| Publications | `_data/publications.yml` | **weekly from Semantic Scholar** |
| Publications to never add | `_data/publications_exclude.yml` | hand |
| Projects page + home carousel | `_data/software.yml`, `_data/carousel.yml` | **weekly from a Google Form** (hand edits also kept) |
| Project research themes | `_data/research_themes.yml`, `_data/research_theme_aliases.yml` | hand |
| Talks & Teaching | `_outreach/talks.md`, `_outreach/teaching.md` (or a Google Sheet) | on every deploy |

Empty sections (alumni, undergrads, carousel, etc.) are hidden until they have entries.

## One-time setup

1. **Turn on Pages:** repo Settings → Pages → Source: **GitHub Actions**. Every push to `main` then
   builds and deploys the site (`.github/workflows/jekyll-gh-pages.yml`).
2. **Fill in `_config.yml`** and replace the `TODO` placeholders in `_pages/home.md`, `_pages/positions.md`,
   `_data/pi.yml` and `_data/research_themes.yml`.
3. **Publications (Semantic Scholar):** in Settings → Secrets and variables → Actions, add:
   - Variable `PI_NAME`: the PI's name exactly as it appears on Semantic Scholar.
   - Variable `LAB_START_DATE`: `YYYY-MM-DD`; papers before this date are ignored.
   - Variable `S2_AUTHOR_ID` (recommended): the number in the PI's Semantic Scholar author URL. When set,
     the sync adds only papers listed on that profile, so other people with the same name are never included.
     Without it, the sync searches by `PI_NAME`, which can pick up namesakes.
   - Secret `S2_API_KEY` (recommended): a free key from
     https://www.semanticscholar.org/product/api#api-key-form. Without it, requests are heavily rate-limited.

   Then run **Actions → Update Publications from Semantic Scholar → Run workflow** once to fill the list.
   Until `PI_NAME` is set, the weekly job skips without failing.
4. **Projects (Google Form):** create a Google Form whose questions use these titles (aliases are listed at
   the top of `scripts/update_projects_from_google_form.py`):
   `Short Title / Acronym`, `Description`, `Publication Date`, `Research Theme` (checkboxes whose options match
   `_data/research_themes.yml`), optional `Website` / `Demo` / `Code` / `Data` / `Paper` links,
   `Project Logo (square image)`, and, for the home carousel, `Project Landscape Summary Figure` and
   `<10 Word Summary / Catchphrase`. A project appears in the carousel only if it has a figure, a summary
   and a Paper link. Image uploads/links on Google Drive must be shared as "anyone with the link".
   Link the form to a Google Sheet, then File → Share → Publish to web → that sheet as CSV. Save the CSV URL
   as Actions variable `PROJECTS_SHEET_CSV_URL`.
5. **Talks & Teaching (optional Google Sheet):** add rows to the tables in `_outreach/*.md`, or put a
   published-CSV URL in their `google_sheet_csv` front matter (columns: Title, Speakers, Host, Date, External).
   Rows from both are merged on each deploy.
6. **Custom domain (optional):** set it in Settings → Pages, then set `url` to it in `_config.yml`.

The publication and project jobs run on Mondays (09:00 and 09:30 UTC), commit any changes and trigger a
redeploy. Both can also be run by hand from the Actions tab.

## Fixing publications

- **Wrong paper (e.g. a different person with the same name):** delete it from `_data/publications.yml`
  *and* add its DOI or title to `_data/publications_exclude.yml`, or the next sync adds it back.
- **Missing paper:** add it to `_data/publications.yml` by hand (template at the top of the file).
  The sync never removes or overwrites existing entries.

## Running locally

```sh
gem install jekyll
pip install pyyaml requests     # only needed to run the scripts
python3 scripts/build_outreach_data.py
jekyll serve                    # http://localhost:4000/
```

Restart `jekyll serve` after editing `_config.yml`.
