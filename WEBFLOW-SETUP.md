# Put the tool on reozix.com/tools/aimetadataremover

GitHub stays the home of the tool. The Webflow page only holds a small snippet that loads the
tool from GitHub, so every update pushed here shows up on reozix.com automatically.

## One-time setup in Webflow (about 10 minutes)

1. **Create the page**
   Pages → + New page → Name: `AI Metadata Remover`, Slug: `aimetadataremover`.

2. **SEO settings** (Page settings → SEO)
   - Title: `Free AI Metadata Remover | Reozix — Private Client-Side Tool`
   - Meta description: `Remove AI metadata from images in bulk. Strip ChatGPT, Midjourney and Firefly tags, C2PA, EXIF, GPS and prompts. Free, private, client-side tool by Reozix.`

3. **Open Graph** (Page settings → Open Graph)
   - Title and description: same as above
   - Image: upload `og-image.png` from this repo

4. **Head code** (Page settings → Custom code → Inside `<head>` tag)
   Paste everything from [`embed/webflow-head.html`](embed/webflow-head.html).

5. **Add the tool**
   - In the Designer, add a Section (between your nav and footer) and drop an **Embed** element (Add → Components → Code Embed) inside it.
   - Paste everything from [`embed/webflow-body.html`](embed/webflow-body.html) and save.
   - The snippet already has the page's H1, so don't add another heading to this page.

6. **Publish** to reozix.com.

7. **Check the canonical tag**
   Open the live page → right-click → View page source → search for `canonical`.
   It must be `https://reozix.com/tools/aimetadataremover`.
   If it points to the homepage, fix it in Site settings → SEO → Global canonical tag URL: `https://reozix.com`.

8. **Google Search Console** → URL inspection → paste the new URL → Request indexing.

## How the two copies work together

| | GitHub Pages | reozix.com |
|---|---|---|
| URL | `shahriar-008.github.io/aimetadataremover` | `reozix.com/tools/aimetadataremover` |
| Role | Source code + direct web version | Main page for Google and sharing |
| Canonical | points to reozix.com | itself |
| Visitor counter | shared | shared |

## Making changes later

1. Edit `index.html` (the GitHub Pages version).
2. Run `python tools/build-embed.py` to rebuild the files in `embed/`.
3. Commit and push. The tool on reozix.com updates within ~10 minutes.

You only need to paste into Webflow again if the SEO text (FAQ, headings) changes.
Logic and tool layout changes update automatically.
