# Nate Korth, Ph.D. — personal website

A plain HTML/CSS academic website. There is no build step: edit an `.html` file, save it, and refresh the page.

```
index.html          Home (photo, bio, the gut-to-soil story, research interests)
research.html       GERMs framework and three research interests
publications.html   Peer-reviewed articles
news.html           LinkedIn post embeds
cv.html             CV summary and PDF download button
contact.html        Email, ORCID, LinkedIn, GitHub
css/style.css       All colors, fonts and layout (colors are at the top)
images/             Web-sized photos and figures used by the pages
files/              Put Korth_CV.pdf here
originals/          Full-size photos and the retired Teaching page (not uploaded; see .gitignore)
```

## Before going live: fill in the TODOs

Search the `.html` files for `TODO` to find each one:

- **CV PDF:** export your CV as `files/Korth_CV.pdf`. Until you do, the download button on the CV page won't work.
- **DOIs:** four older papers in `publications.html` have no DOI link yet.
- Optional: Google Scholar link, manuscripts in preparation.

The menu is repeated at the top of every page. To rename or add a page, change it in all six `.html` files.

## Adding photos

Phone photos are 3–5 MB, which makes pages slow on phones. Before adding one, shrink it to about 1600 pixels on the long side (for example with Windows Photos → Resize, or ask Claude). Keep the full-size original in `originals/`.

## Preview on your computer

From this folder:

```bash
python -m http.server 8000
```

Then open http://localhost:8000 in a browser. Press Ctrl+C to stop the server.

## 1. Publish on GitHub Pages (free)

Your site will be at **https://natekorth.github.io**.

1. Sign in to GitHub as **NateKorth** and create a new repository named exactly `NateKorth.github.io`. Make it **Public** and do not add a README (this folder already has one).
2. In this folder, run:

   ```bash
   git init
   git add .
   git commit -m "First version of personal website"
   git branch -M main
   git remote add origin https://github.com/NateKorth/NateKorth.github.io.git
   git push -u origin main
   ```

3. On GitHub, open the repo, then **Settings → Pages**. Under "Build and deployment", set the Source to **Deploy from a branch**, the branch to **main**, and the folder to **/ (root)**. Save.
4. After about a minute, the site is live at https://natekorth.github.io.

To update the site later, edit the files and run:

```bash
git add .
git commit -m "Describe the change"
git push
```

## 2. Optional: use a custom domain (e.g. natekorth.com)

1. Buy the domain from a registrar such as Cloudflare, Porkbun, Namecheap or Squarespace Domains (about $10–15/year).
2. On GitHub, go to the repo's **Settings → Pages → Custom domain**, enter `natekorth.com` and save. GitHub adds a `CNAME` file to the repo; run `git pull` afterward so your copy has it too.
3. At your registrar, add these DNS records:
   - Four **A** records for `@` (the bare domain), pointing to:
     `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - One **CNAME** record for `www`, pointing to `natekorth.github.io`
4. Wait for DNS to update (usually under an hour, sometimes up to a day). Then, back in **Settings → Pages**, tick **Enforce HTTPS**.

GitHub's guide: https://docs.github.com/pages/configuring-a-custom-domain-for-your-github-pages-site

## 3. Add a LinkedIn post to the News page

LinkedIn has no official widget for showing your whole feed, so you embed individual posts.

1. On LinkedIn, open the post. Click the **…** menu at its top right and choose **Embed this post**. (This option only appears for public posts.)
2. Click **Copy code**. You'll get something like:

   ```html
   <iframe src="https://www.linkedin.com/embed/feed/update/urn:li:share:7123456789" height="600" width="504" frameborder="0" allowfullscreen="" title="Embedded post"></iframe>
   ```

3. Open `news.html`. Each post is a block like this:

   ```html
   <div class="post">
     <iframe src="https://www.linkedin.com/embed/feed/update/..." height="924" width="504" ...></iframe>
   </div>
   ```

   Copy one whole block, paste it where you want the new post (newest first), and replace the `<iframe ...></iframe>` line with the code you copied. The iframe goes directly inside `<div class="post">`, with nothing else in the box.
4. Delete the block for any post you want to remove. Three to five posts works well.
5. If a post looks cut off, raise the `height="..."` number in its code.
