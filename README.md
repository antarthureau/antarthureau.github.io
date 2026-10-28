# antart

Personal site of Antoine Hureau-Parreira: about, teaching, works, music, code, services and a blog. Built with Jekyll and published with GitHub Pages. It replaces antart.no.

## Where things live

| To change | Edit |
| --- | --- |
| Site title, description, sidebar roles, portrait, URL | `_config.yml` |
| Front page text | `index.md` |
| Menu | `_data/navigation.yml` |
| Footer links | `_data/links.yml` |
| About and UiB role | `about.md` |
| Courses (current and earlier) | `_data/teaching.yml` |
| Selected works (project pages and front-page grid) | `_works/` |
| Full works list | `_data/works.yml` |
| Music: platforms, albums, tracks, Spotify player | `_data/music.yml` |
| Featured repositories | `_data/projects.yml` |
| Services | `services.md` |
| Blog posts | `_posts/` |
| Unpublished drafts | `_drafts/` |
| Photos | `assets/img/` |
| Colours and type | `assets/css/main.scss` |

Every public repository that is not featured or listed in `hide_repos` in `_config.yml` is shown automatically on `/code/` when GitHub Pages builds the site.

## Adding photos

Images appear as soon as the file exists at the path the site expects, so you only need to drop files in and commit:

| Photo | File | Size |
| --- | --- | --- |
| Portrait (sidebar) | `assets/img/portrait.jpg` | square, about 600 × 600 px |
| Suuret muinaiset päiväunilla | `assets/img/works/suuret-muinaiset.jpg` | 4:3, about 1600 × 1200 px |
| PRODROME | `assets/img/works/prodrome.jpg` | 4:3 |
| The Tempest | `assets/img/works/the-tempest.jpg` | 4:3 |
| Lyttekammers | `assets/img/works/lyttekammers.jpg` | 4:3 |

Until a photo is there, its tile shows a plain grey block with the work's medium. Keep files under about 400 KB (export as JPEG at 80% quality). To credit a photographer, set `photo_credit` in `_config.yml` for the portrait, or `image_credit` in a work's front matter.

## Adding a selected work

Copy one of the files in `_works/`, rename it (the file name becomes the address, e.g. `_works/hydra.md` → `/works/hydra/`) and edit its front matter:

```yaml
---
title: Hydra
year: "2018"
place: Rom 8, Bergen, NO
collaborators: Craig Wells
medium: sound installation
image: /assets/img/works/hydra.jpg
featured: true      # show in the grids
order: 5            # position in the grids
links:
  - title: Project site
    url: https://beepblipbuzz.com/
---

Text about the work in Markdown.
```

The front page shows the first four featured works; the works page shows all of them.

## Writing a post

Create `_posts/YYYY-MM-DD-short-title.md`:

```markdown
---
title: a short title
description: One sentence for search engines and link previews.
tags: [teaching, pure data]
---

Text in Markdown.
```

Commit and push. GitHub rebuilds the site in a minute or two.

To edit directly on GitHub: open the repository, press `.` to open the web editor, or use **Add file → Create new file** inside `_posts/`.

## Publishing on GitHub Pages

1. Create a repository called `antarthureau.github.io` (or reuse the existing one; see below).
2. Push this folder to its `main` branch:
   ```sh
   cd ~/Documents/GitHub/blog
   git init -b main
   git add .
   git commit -m "New site"
   git remote add origin https://github.com/antarthureau/antarthureau.github.io.git
   git push -u origin main
   ```
3. In the repository, go to **Settings → Pages**, set **Source** to **Deploy from a branch**, branch `main`, folder `/ (root)`.

The site is then at https://antarthureau.github.io.

### If antarthureau.github.io already holds the old Chirpy site

Either rename the old repository first (Settings → General → Repository name, e.g. `old-chirpy-site`) and create a fresh `antarthureau.github.io`, or replace its contents with this folder and force-push. Chirpy builds with a GitHub Actions workflow; if you reuse the repository, delete `.github/workflows/` and switch **Settings → Pages → Source** back to **Deploy from a branch**.

### Using another repository name

The settings in `_config.yml` assume the repository is named `antarthureau.github.io`. Under any other name (for example `blog`), GitHub serves the site at https://antarthureau.github.io/blog/ and every link and the stylesheet break. Either rename the repository (Settings → General → Repository name) to `antarthureau.github.io`, or set `baseurl: "/blog"` in `_config.yml`.

After a rename, point your local copy at the new name with `git remote set-url origin https://github.com/antarthureau/antarthureau.github.io.git` (GitHub also redirects the old address).

## Keeping antart.no

To point antart.no at this site instead of closing the domain:

1. Add a file named `CNAME` at the root of the repository containing `antart.no`.
2. At your DNS provider, create A records for `antart.no` pointing to `185.199.108.153`, `185.199.109.153`, `185.199.110.153` and `185.199.111.153`, and a CNAME record for `www` pointing to `antarthureau.github.io`.
3. In **Settings → Pages**, enter `antart.no` as the custom domain and tick **Enforce HTTPS** once the certificate is issued.
4. Set `url: "https://antart.no"` in `_config.yml`.

Check GitHub's current instructions before changing DNS: https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site

## Running it locally

Requires Ruby 3 and Bundler.

```sh
bundle install
bundle exec jekyll serve --livereload
```

Open http://localhost:4000. Add `--drafts` to preview posts in `_drafts/`.
