# How We Learn — Interactive 3D Map

An animated, rotatable 3D mind map built with Three.js. Click the center
node to expand it into the four learning theories (Behaviorism, Cognitivism,
Constructivism, Connectivism), click a theory to reveal its theorists and
concepts, and click any point to open its picture + description in the side
panel. Drag to spin the whole cloud, scroll to zoom.

Source content: Dorian Peters, *Interface Design for Learning*, Chapter 2:
"How We Learn" (UXmatters, 2014).

## Publishing it on GitHub Pages

1. Create a new repository on GitHub (public — GitHub Pages on the free
   tier requires a public repo).
2. Upload the contents of this folder to the repo:
   - Easiest no-install option: on the repo's main page, click
     **Add file → Upload files**, then drag in `index.html`, `README.md`,
     and the `images` folder (with your pictures in it, if you've added
     any), and commit.
   - Or, if you use git locally: `git add . && git commit -m "Add map" && git push`.
3. In the repo, go to **Settings → Pages**.
4. Under **Build and deployment → Source**, choose **Deploy from a branch**,
   pick the `main` branch and the `/ (root)` folder, then **Save**.
5. GitHub will give you a live URL (usually
   `https://<your-username>.github.io/<repo-name>/`) within a minute or two.
   That's the link to submit.

**Important:** the file must be named `index.html` (it already is) so GitHub
Pages serves it automatically at that URL. If you rename it, the site will
404 unless visitors add the filename to the link.

## Editing the content

Open `index.html` in any text editor and find the `const data = { ... }`
object near the top of the `<script type="module">` block. Every node in
the map (the center, each theory, each theorist/concept) is an object with:

- `name` — the title shown under the point and at the top of the side panel
- `detail` — the description shown in the side panel
- `color` — the accent color for that node's branch
- `emoji` — used to generate the default placeholder icon
- `image` — set to `null` to use the generated placeholder, or to a path/URL
  to use a real photo instead (see below)

Edit `name` and `detail` directly to change the text for any node — no other
code needs to change.

## Adding real images

Set a node's `image` field to a path, e.g.:

```js
{ name: "Ivan Pavlov", color: COLORS.behaviorism, emoji: "🔔",
  image: "images/pavlov.jpg",
  detail: "Classical conditioning — ..." }
```

Drop your picture files into the `images/` folder in this package (create
it if it isn't there) and reference them with a relative path like
`images/pavlov.jpg`, exactly matching the filename.

Any image works — the code automatically center-crops it to a square and
masks it into the same circular, ringed style as the placeholders, so you
don't need to pre-crop anything. If an image path is wrong or fails to
load, that node just keeps its emoji placeholder instead of breaking.

If you link to an image hosted elsewhere instead of putting it in this
repo, some external hosts don't allow the crop step (a CORS restriction).
Keeping images inside this repo's `images/` folder avoids that entirely.
