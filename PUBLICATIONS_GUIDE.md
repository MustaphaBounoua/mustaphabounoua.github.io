# Publications Guide

This guide explains how to manage your publications with preview images, PDFs, code, and slides.

## Structure

Your publications are organized by **year** in descending order on the `/publications/` page. Each publication entry can include:

- **Preview Image**: Thumbnail representing the paper
- **PDF**: Link to the full paper
- **Slides**: Presentation slides
- **Code**: GitHub repository or code link
- **Abstract**: Paper abstract
- **BibTeX**: Citation information

## Adding Publication Preview Images

### Step 1: Prepare Your Image
Create a preview image (recommended: 200x200px or 300x300px, or larger if you want a more prominent thumbnail). The stylesheet now allows up to **400px** width for publication previews. Save it with a descriptive name:
```
ddmec.png          (already exists as example)
tende.png          (for munoz paper)
somegai.png        (for SΩI paper)
minde.png          (for MINDE paper)
```

### Step 2: Upload to Assets Folder
Upload preview images to:
```
assets/img/publication_preview/
```

### Step 3: Update BibTeX Entry
In `_bibliography/papers.bib`, add the `preview` field:

```bibtex
@inproceedings{example2025,
  title={Your Paper Title},
  author={Your Name},
  booktitle={Conference Name},
  year={2025},
  preview={your_image.png},  // Just the filename
  pdf={https://example.com/paper.pdf},
  code={https://github.com/yourname/repo},
  slides={https://example.com/slides.pdf}
}
```

## BibTeX Fields Reference

### Supported Fields in Publications

| Field | Purpose | Example |
|-------|---------|---------|
| `preview` | Thumbnail image filename | `ddmec.png` |
| `pdf` | Link to full paper (URL or local) | `https://arxiv.org/pdf/...` |
| `code` | GitHub or code repository link | `https://github.com/user/repo` |
| `slides` | Presentation slides link | `https://example.com/slides.pdf` |
| `abstract` | Paper abstract | `This paper proposes...` |
| `arxiv` | arXiv paper ID | `2310.14096` |
| `bibtex_show` | Show BibTeX citation button | `true` |
| `presentation_type` | Type of presentation | `oral` or `poster` |
| `abbr` | Conference abbreviation | `ICML` |
| `doi` | Digital Object Identifier | `10.3390/e26040320` |

## Example Publications

### Complete Entry with All Fields
```bibtex
@inproceedings{bounoua2025example,
  title={Complete Example Paper},
  author={Mustapha Bounoua and Co-Author Name},
  booktitle={International Conference Name},
  year={2025},
  abbr={ICML},
  bibtex_show={true},
  presentation_type={oral},
  preview={example.png},
  pdf={https://openreview.net/pdf?id=...},
  code={https://github.com/MustaphaBounoua/example},
  slides={https://example.com/slides.pdf},
  abstract={This is the paper abstract...}
}
```

## Publishing Your Changes

After updating `papers.bib` or adding preview images:

1. Local testing (if using Docker):
   ```bash
   bin/docker_run.sh bundle exec jekyll serve
   ```

2. Push to GitHub:
   ```bash
   git add _bibliography/papers.bib assets/img/publication_preview/
   git commit -m "Add publication previews and details"
   git push origin master
   ```

The website will automatically rebuild on GitHub Pages.

## Organizing By Year

Publications are automatically grouped by year in **descending order** (newest first). You don't need to manually organize them - just ensure each entry has the correct `year` field.

## Styling Tips

- **Preview images**: Square format (1:1 ratio) works best and displays nicely in the 2-column grid
- **PDF links**: Can be URLs (https://...) or local files in `assets/pdf/`
- **Code links**: GitHub links display with a "Code" button
- **Multi-author papers**: You can use markdown like `Author One and Author Two` or use `*` for equal contribution: `First Author$^*$ and Second Author$^*$`

## Current Publication Status

All entries in your `papers.bib` have been updated with fields for:
- ✅ Preview images (empty, ready for upload)
- ✅ PDF links
- ✅ Code links (where available)
- ✅ Slides (empty, ready to add)

Just upload the preview images and fill in the missing URLs!
