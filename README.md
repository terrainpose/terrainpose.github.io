# TerrainPose project website

## What is included

- `index.html`: one scrolling project page with six sections, green accent `#3e7429`, the requested text, an inactive Paper link, six image links, and one video player.
- `README.md`: these instructions.

The image and video files were not supplied with this request and are **not included**. Missing assets produce clearly labeled placeholders. They are not replaced with invented figures.

The layout follows the reference's research-project structure: https://seohong.me/projects/fql/. The HTML and CSS were written independently.

## 1. Put your media beside the HTML

Arrange your files exactly like this:

```text
terrainpose_site/
├── index.html
├── README.md
├── figure1.png
├── figure_distillation.png
├── Student_network.png
├── Teacher_network.png
├── figure4.png
├── figure5.png
└── run1.mp4
```

The capital `S` in `Student_network.png` and capital `T` in `Teacher_network.png` matter on case-sensitive filesystems, including typical Linux setups.

All media paths in the supplied HTML are already set to these filenames. No HTML edits are necessary with this folder arrangement. After adding the files, reload the browser page.

## 2. Open the page

Double-click `index.html`, or right-click it and choose your browser. The file can be viewed directly from the local filesystem.

For a local web-server preview, open a terminal in this folder and run:

```bash
python3 -m http.server 8000 --bind 127.0.0.1
```

Then visit:

```text
http://127.0.0.1:8000/
```

Stop the server with `Ctrl+C`. This is a local preview server, not a production hosting setup. Serve this project folder, not a folder containing unrelated private files.

The HTML uses system fonts, embedded CSS/JavaScript, and native MathML. It makes no external network requests and does not require MathJax, Google Fonts, npm, or an internet connection. Use a modern browser with MathML support (for example current Chrome, Firefox, Edge, or Safari).

## 3. Use subfolders instead

For this layout:

```text
terrainpose_site/
├── index.html
├── images/
│   ├── figure1.png
│   ├── figure_distillation.png
│   ├── Student_network.png
│   ├── Teacher_network.png
│   ├── figure4.png
│   └── figure5.png
└── videos/
    └── run1.mp4
```

Update the relevant paths in `index.html`:

```html
<a class="figure-link" href="images/figure1.png" target="_blank" rel="noopener">
  <img src="images/figure1.png" alt="TerrainPose overview">
</a>

<video src="videos/run1.mp4" controls playsinline preload="metadata">
  Your browser does not support HTML video.
  <a href="videos/run1.mp4">Open the video</a>.
</video>
```

Change each image's `src` and matching link's `href`. The included JavaScript also synchronizes image links with their image paths automatically. Image placeholders display the path actually specified in `src`.

Paths are relative to `index.html`. A leading `/` means the server root, not the folder beside the page. Do not use `~`, which HTML does not expand into your home folder.

## 4. Keep files elsewhere on your computer

The most portable arrangement is to put the actual media inside the project folder. To avoid moving the original files, you can copy them there. For example, from the project folder:

```bash
cp /path/to/your/figures/figure1.png ./figure1.png
cp /path/to/your/videos/run1.mp4 ./run1.mp4
```

On Linux, a symbolic link is another option for a local preview, especially for a large video:

```bash
ln -s /absolute/path/to/run1.mp4 ./run1.mp4
```

A symbolic link does not embed or copy the video. The original file must remain accessible. Replace such links with the actual media files before sharing or deploying the folder; otherwise other computers will not have the target files. Python's local `http.server` follows symbolic links, so create links only to files you intend to serve.

Do not put `/home/...` or `file:///...` paths in a public project page: those are paths on your own computer, not public website URLs. Upload the images and video with the HTML when publishing it.

## 5. Enable the Paper link later

Search for `PAPER LINK` in `index.html`. Replace this opening tag:

```html
<a class="paper-link is-disabled" role="link" aria-disabled="true" aria-describedby="paper-state" tabindex="0">
```

with:

```html
<a class="paper-link" href="paper.pdf" target="_blank" rel="noopener">
```

Keep the SVG icon, Paper text, and closing `</a>` tag. Put `paper.pdf` beside `index.html`. Alternatively, set `href` to the paper's public URL. Delete this line:

```html
<p class="paper-state" id="paper-state">Link coming soon</p>
```

## 6. Change styling or content

At the top of the `<style>` block:

```css
:root {
  --accent: #3e7429;
  --page-width: 920px;
}
```

The accent controls headings, bullets, links, the Paper button, and the conclusion box's side border. Change `--page-width` to make the article column wider or narrower.

Each section is labeled `PAGE 1` through `PAGE 6` in HTML comments. These are sections of one scrolling page, not six separate HTML documents or fixed-height slide panels.

The PnP equation is rendered using MathML for offline viewing. Its original LaTeX is preserved in a comment immediately above the MathML. Editing that comment alone will not change the rendered equation; edit the MathML too. Inline `F_{IG}` also uses MathML. Numeric values and units use regular HTML text.

## Content notes

- The three Overview bullets were drafted from the method description supplied in the request, since exact overview bullet text was not provided.
- The request referred to `eq:terrain_corrected_pose` without supplying that equation. The webpage instead says the translation is corrected according to the terrain elevation map. No correction equation was invented.
- The extra `m` after `2.84 m` was removed. Research numbers were otherwise retained as supplied.
- Minor punctuation, articles, and hyphenation were cleaned up; no authors or affiliations were added.

## Troubleshooting

**An image placeholder appears:** Check the exact filename, capitalization, extension, and its path relative to `index.html`, then refresh the page. The images are linked, not embedded in the HTML.

**A video placeholder appears:** Check that `run1.mp4` exists at the specified path and that the browser can decode the video. An `.mp4` extension identifies a container, not necessarily a supported codec. H.264 video in MP4 is a common browser-compatible choice. A local server can help distinguish path issues from playback issues.

**The content is visible but a figure is too small:** Click a loaded figure to open it at full resolution. The page preserves the image's natural proportions; it does not crop the figure.

**The formula looks different on another computer:** Native MathML uses the browser and locally available mathematical fonts. The exact font can vary across systems. No font files are distributed with this page.

## Technical references

- Relative image paths: https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Structuring_content/HTML_images
- Native MathML: https://developer.mozilla.org/en-US/docs/Web/MathML
- Local Python preview server: https://docs.python.org/3/library/http.server.html
- HTML video: https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/video
