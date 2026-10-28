# antart

Personal site of Antoine Hureau-Parreira: about, teaching, works, music, code, services and a blog. Built with Jekyll and published with GitHub Pages. It replaces antart.no.

## Where things live

| To change | Edit |
| --- | --- |
| Site title, description, photo, URL | `_config.yml` |
| Front page text | `index.md` |
| Menu | `_data/navigation.yml` |
| Footer links | `_data/links.yml` |
| About and UiB role | `about.md` |
| Courses (current and earlier) | `_data/teaching.yml` |
| Works list | `_data/works.yml` |
| Music: platforms, albums, tracks, Spotify player | `_data/music.yml` |
| Featured repositories | `_data/projects.yml` |
| Services | `services.md` |
| Blog posts | `_posts/` |
| Unpublished drafts | `_drafts/` |
| Colours and type | `assets/css/main.scss` |

Every public repository that is not featured or listed in `hide_repos` in `_config.yml` is shown automatically on `/code/` when GitHub Pages builds the site.

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

If the repository is called something else (for example `blog`), set `baseurl: "/blog"` in `_config.yml`. The site will be at https://antarthureau.github.io/blog/.

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
