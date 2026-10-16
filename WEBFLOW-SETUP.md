# Put the tool on www.designmonks.co/aimetadataremover

GitHub stays the home of the tool. The Webflow page only holds a small snippet that loads the
tool from GitHub, so every update pushed here shows up on designmonks.co automatically.

## One-time setup in Webflow (about 10 minutes)

1. **Create the page**
   Pages → + New page → Name: `AI Metadata Remover`, Slug: `aimetadataremover`.

2. **SEO settings** (Page settings → SEO)
   - Title: `Free AI Metadata Remover: Remove AI Info from Images`
   - Meta description: `Remove AI metadata from images in bulk. Strip ChatGPT, Midjourney and Firefly tags, C2PA, EXIF, GPS and prompts. Free, private, no upload, same quality.`

3. **Open Graph** (Page settings → Open Graph)
   - Title and description: same as above
   - Image: upload `og-image.png` from this repo

4. **Head code** (Page settings → Custom code → Inside `<head>` tag)
   Paste everything from [`embed/webflow-head.html`](embed/webflow-head.html).

5. **Add the tool**
   - In the Designer, add a Section (between your nav and footer) and drop an **Embed** element (Add → Components → Code Embed) inside it.
   - Paste everything from [`embed/webflow-body.html`](embed/webflow-body.html) and save.
   - The snippet already has the page's H1, so don't add another heading to this page.

6. **Publish** to designmonks.co.

7. **Check the canonical tag**
   Open the live page → right-click → View page source → search for `canonical`.
   It must be `https://www.designmonks.co/aimetadataremover`.
   If it points to the homepage, fix it in Site settings → SEO → Global canonical tag URL: `https://www.designmonks.co`.

8. **Google Search Console** → URL inspection → paste the new URL → Request indexing.

## How the two copies work together

| | GitHub Pages | designmonks.co |
|---|---|---|
| URL | atiq31416.github.io/aimetadataremover | www.designmonks.co/aimetadataremover |
| Role | Source code + backup copy | Main page for Google and sharing |
| Canonical | points to designmonks.co | itself |
| Visitor counter | shared | shared |

## Making changes later

1. Edit `index.html` (the GitHub Pages version).
2. Run `python3 tools/build-embed.py` to rebuild the files in `embed/`.
3. Commit and push. The tool on designmonks.co updates within ~10 minutes.

You only need to paste into Webflow again if the SEO text (FAQ, headings) changes.
Logic and tool layout changes update automatically. If browsers keep an old style after a big
change, bump `v = '1'` in `tools/build-embed.py` and re-paste the body snippet.
