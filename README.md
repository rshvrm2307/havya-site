# Havya Corp — static site

Plain HTML/CSS/JS. No build step, no dependencies.

Audience: individuals and small businesses — people building data pipelines, learning to
use AI day to day and in their own projects, and one-on-one yoga students.

```
index.html          Overview / home
contact.html        Email-only contact page (no form — add one later if wanted)
blog.html           Blog index (empty state for now)
assets/css/style.css
assets/js/main.js
.nojekyll           Tells GitHub Pages to serve files as-is
```

## Preview locally

Open `index.html` in a browser, or serve it so paths behave exactly like they will live:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Publish on GitHub Pages

Full walkthrough — including the browser-only route (no terminal) and the custom-domain DNS
setup: **[DEPLOY.md](DEPLOY.md)**.

Short version, if you're comfortable with git:

1. Create a repo on GitHub. For a URL like `https://<username>.github.io`, name it
   `<username>.github.io`. Any other name gives you `https://<username>.github.io/<repo>/`.
2. Copy these files into the repo root (not inside a subfolder), then:

   ```bash
   git init
   git add .
   git commit -m "Initial site"
   git branch -M main
   git remote add origin https://github.com/<username>/<repo>.git
   git push -u origin main
   ```
3. In the repo: **Settings → Pages → Build and deployment**. Source = *Deploy from a
   branch*, Branch = `main`, Folder = `/ (root)`. Save.
4. Wait ~1 minute, then load the URL Pages shows you.

Every later `git push` to `main` republishes automatically.

## Before you go live — things to change

| What | Where |
|---|---|
| Brand colors and fonts | `:root` block at the top of `assets/css/style.css` |
| Service copy | `index.html`, `#services` section |
| "Who this is for" bullets | `index.html`, `.audience` list |
| Business name "Havya Corp" | header, footer and `<title>` of all three HTML files |

No email address or social link is published anywhere on the site right now — that's
deliberate, since neither exists yet. Nothing on the live site points at a dead address.

## Switching the email on

Once the mailbox actually receives mail:

1. Open `contact.html`. Delete the `<div class="notice">` block ("Contact details coming
   soon") and uncomment the `LIVE CONTACT` section directly below it.
2. In `index.html`, `blog.html` and `contact.html`, uncomment the footer email line.
3. Replace every `you@yourdomain.com` with the real address:

   ```bash
   grep -rl you@yourdomain.com *.html \
     | xargs sed -i '' 's/you@yourdomain.com/hello@yourrealdomain.com/g'
   ```
4. Same idea for social profiles: `contact.html` has a commented-out "Follow along" list —
   uncomment it, delete the platforms you don't use, and replace each `#` with a real URL.

### Adding a contact form later

GitHub Pages serves static files only — it cannot process a form POST, so a form needs a
third-party endpoint. [Formspree](https://formspree.io) is the usual choice: sign up,
create a form, and point `<form action="https://formspree.io/f/YOUR_ID" method="POST">` at
it. Alternatives: Google Forms embed, or Netlify Forms (means hosting on Netlify instead of
Pages). For now the contact page just links to email, which needs nothing.

## Adding your first blog post

1. Copy `blog.html` to `posts/my-first-post.html` and replace the main section with your
   article.
2. In `blog.html`, delete the `.empty-state` block and uncomment the `.post-list` block
   right below it, then fill in the title, date, and summary.

## Custom domain

See [DEPLOY.md](DEPLOY.md) — Part 2 covers pointing a Wix-registered domain at GitHub Pages,
including the exact DNS records and the Wix-specific gotchas.
