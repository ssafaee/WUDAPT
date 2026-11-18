# Instructions

## 1. Upload to GitHub

1. Sign in at github.com and click **+ → New repository**.
2. Name it (for example `wudapt-india-atlas`), choose **Public**, tick **Add a README file**, and click **Create repository**.
3. In the new repository, click **Add file → Upload files**.
4. Unzip `wudapt-india-atlas-github.zip` on your computer. Open the folder and drag **everything inside it** into the upload box: `index.html`, `README.md`, `INSTRUCTIONS.md` and the `scripts` folder. Drag the contents, not the outer folder. If GitHub asks, replace its README with this one.
5. Click **Commit changes**.

## 2. Turn on the website (GitHub Pages)

1. In the repository, go to **Settings → Pages**.
2. Under **Build and deployment**, choose **Deploy from a branch**, select **main** and **/ (root)**, then click **Save**.
3. After a minute or two, the address appears at the top of the Pages screen:
   `https://YOUR-USERNAME.github.io/REPO-NAME/`
4. Add that address to `README.md` and to the repository's **About → Website** field.

Pages is free for public repositories. Private repositories need a paid GitHub plan.

## 3. View on your computer

1. On GitHub, open `index.html` and click **Download raw file**.
2. Double-click the downloaded file. No internet connection or installation is needed.

The file is about 20 MB, so it may take a few seconds to open. GitHub will say the file is too big to display its code, which is normal.

## 4. Use the viewer

- **Find a city:** click a dot on the map, type a name in **Find a city**, or click a row in **All cities, side by side**.
- **Move between cities:** use the ← and → buttons, or the arrow keys.
- **Enlarge a map sheet:** click it. Press **Esc** to close it.
- **Change the map colours:** use **Colour dots by**.
- **Share a city:** add its name to the address, for example `…/#chennai` or `…/#new-delhi`.

## 5. Rebuild after changing the atlas (advanced)

You need the atlas Word document (`.docx`), which is not in the repository because of its size.

**Requirements:** Python 3 and [Tesseract OCR](https://github.com/tesseract-ocr/tesseract) (used to read chart axes). Then install the Python packages:

```
pip install -r scripts/requirements.txt
```

**Rebuild** from the repository folder:

```
python scripts/build_all.py path/to/atlas.docx
```

This replaces `index.html` with a new version. Intermediate files go to a `build` folder, which you can delete afterwards.

What each script does:

| Script | Step |
|---|---|
| `parse2.py` | Reads the document's text and images in order. |
| `cities.py` | Splits the document into cities, each with its map and charts. |
| `bars.py`, `runbars.py` | Measure each bar chart to get zone shares and areas. |
| `facts.py` | Extracts area, population, rainfall and coordinates from the text. |
| `build.py` | Writes the city data and compresses the map images. Coordinate corrections are listed here. |
| `make_single.py` | Combines everything into the single-file `index.html`. |
| `assets/template.html` | The viewer's design and code, before the data is added. Edit this to change the page. |
| `assets/india.json` | The India outline used on the map. |
