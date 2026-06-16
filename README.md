# Nick Fraser — personal site

A five-page Jekyll site (Home, About, Projects, Blog, Reading), hosted
free on **GitHub Pages** and edited free with **Pages CMS**
(app.pagescms.org). No coding needed after the initial setup.

This README also notes how to move to Netlify or Cloudflare Pages
later if you ever want to, but you do **not** need to for a custom
domain — see "Custom domain" below.

---

## 1. Create the repo

1. Go to github.com and create a **new public repository** named
   `YOUR-USERNAME.github.io` (replace with your actual GitHub username,
   e.g. `nickfraser.github.io`). This exact naming gives you the clean
   URL `https://YOUR-USERNAME.github.io`.
2. Don't add a README, .gitignore, or license when creating it — leave
   it empty so there's nothing to conflict with.

## 2. Upload these files

1. On the new repo's page, click "uploading an existing file".
2. Open this unzipped folder and drag the **contents** (not the folder
   itself) into the browser window — GitHub preserves subfolders when
   you drag a whole tree in.
3. Commit the changes (the default commit message is fine).

## 3. Set your URL

Open `_config.yml` in the GitHub web editor (click the file, click the
pencil icon) and change:

```yaml
url: "https://YOUR-USERNAME.github.io"
```

to your actual username, then commit.

## 4. Turn on GitHub Pages

1. In your repo, go to **Settings → Pages**.
2. Under "Build and deployment", set **Source** to "Deploy from a
   branch".
3. Set **Branch** to `main` and folder to `/ (root)`, then save.
4. Wait 1–2 minutes, then visit `https://YOUR-USERNAME.github.io`.

GitHub builds Jekyll sites automatically using its own pinned
environment — no Gemfile, no build command, nothing else needed. If the
site doesn't appear, check the **Actions** tab for a build log (almost
always a YAML formatting slip in a front-matter block).

## 5. Connect Pages CMS

This is your editing tool — a form-based interface that writes
directly back to this GitHub repo.

1. Go to **app.pagescms.org** and sign in with GitHub.
2. Authorise the Pages CMS GitHub App, granting it access to this one
   repository.
3. Click "Open a project" and select your repo.
4. It reads the `.pages.yml` already in this site and shows five
   editable sections: **Blog posts**, **Projects**, **Reading**, **Home
   page**, and **About page**.

That's the whole setup. From here on, everything is done through that
interface.

---

## Day-to-day editing

- **Write a blog post**: Pages CMS → Blog posts → New. Title, date,
  body in the rich-text editor, Save. This commits a new file to
  `_posts/`, GitHub rebuilds automatically (~1 minute), and it appears
  on the Blog page and the homepage's "Latest writing" section.
- **Add a project**: Pages CMS → Projects → New. Title, description,
  status (active / growing / idea / archived), optional link, and an
  "Order" number to control its position in the list.
- **Add something you're reading**: Pages CMS → Reading → New. Title,
  author, status (reading / finished / want-to-read), optional notes.
- **Update About**: Pages CMS → About page → edit the body.
- **Tweak the homepage intro**: Pages CMS → Home page → edit the hero
  title, subtitle, and two intro paragraphs. The "Latest writing" and
  "Currently" sections update themselves from your posts and projects.

Every save = a commit = a fresh build, live within a minute or two.

---

## Custom domain (optional, whenever you're ready)

You can attach `nickfraser.nz` (or whatever you choose) to GitHub
Pages directly, for free — no migration to another host required:

1. Buy the domain from any registrar (~NZD 20–35/year for `.nz` or
   `.com` — this is the only ever cost in this whole setup, and it's
   the same regardless of where the site is hosted).
2. In your repo: **Settings → Pages → Custom domain**, enter the
   domain, save.
3. At your registrar, add the DNS records GitHub's docs specify (a few
   A records for the apex domain, or a CNAME if using a `www`
   subdomain).
4. Tick "Enforce HTTPS" once it's available (GitHub provisions a free
   certificate automatically).

Pages CMS keeps working exactly the same — it talks to the GitHub
repo, not the domain.

---

## If you ever want to move to Netlify or Cloudflare Pages instead

Not needed for a custom domain, but if you want it for other reasons
(build features, edge network, etc.), this repo is already set up for
it:

- **Netlify**: Connect the repo at app.netlify.com. The included
  `netlify.toml` sets the build command (`bundle exec jekyll build`),
  output folder (`_site`), and Ruby version automatically — no manual
  config needed.
- **Cloudflare Pages**: Connect the repo in the Cloudflare dashboard,
  choose the Jekyll framework preset (build command `bundle exec jekyll
  build`, output `_site`), and set the environment variable
  `RUBY_VERSION = 3.2.2` to match the included `.ruby-version`.

In both cases, update `url:` in `_config.yml` to the new address, and
Pages CMS needs no changes at all — it's pointed at GitHub regardless
of who's building the site.

---

## Optional: preview locally

```
bundle install
bundle exec jekyll serve
```

Then open `http://localhost:4000`. Not required — GitHub builds and
serves the live site for you.

---

## File structure reference

```
_config.yml        site settings (title, URL, permalinks, markdown)
_layouts/          page templates (default, page, post)
_includes/         nav and footer snippets
assets/css/        stylesheet
assets/images/     upload images here via Pages CMS
_posts/            blog posts (one file per post)
_projects/         project entries shown on Projects + Home
_reading/          reading list entries
index.html         home page
about.md           about page
projects.html      projects listing
blog.html          blog listing
reading.html       reading listing
.pages.yml         Pages CMS configuration — don't need to edit this
Gemfile / .ruby-version / netlify.toml
                    portability files for local preview / Netlify /
                    Cloudflare — safe to leave as-is for GitHub Pages
```
