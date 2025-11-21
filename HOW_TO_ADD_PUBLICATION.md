# How to Add a New Publication

This guide explains the steps to add a new publication to your academic website.

## Step 1: Add Publication to BibTeX File

Edit `_bibliography/papers.bib` and add your new publication entry:

```bibtex
@article{authorYYYYkeyword,
  title={Your Paper Title Here},
  author={Last1, First1 and Last2, First2 and Moon, Jinuk and Others},
  journal={Journal Name},
  volume={XX},
  number={YY},
  pages={XXXX},
  year={2025},
  month={Month},
  publisher={Publisher Name},
  selected={true},  # Set to true if you want it in "Selected Publications"
  preview={authorYYYYkeyword.jpg},  # Preview image filename
  date={2025-MM-DD},  # IMPORTANT: Used for sorting (newest first)
  doi={10.XXXX/xxxxx},  # DOI number
  html={https://doi.org/10.XXXX/xxxxx}  # Full URL to paper
}
```

### Important Fields:
- **date**: Format as `YYYY-MM-DD`. This is used for sorting publications (newest first)
- **selected**: Set to `true` to show in "Selected Publications" on homepage
- **preview**: Image filename (should be placed in `assets/img/publication_preview/`)
- **doi**: DOI number only (without https://doi.org/)
- **html**: Full URL to the paper (alternative to DOI)
- **website**: Project website URL (optional)

### Link Priority:
When users click on the image or title, they will be directed to (in order of priority):
1. DOI link (if available)
2. HTML link (if DOI not available)
3. Website link (if neither DOI nor HTML available)

## Step 2: Add Preview Image

1. Create a preview image for your publication (recommended size: 400x300px or similar aspect ratio)
2. Save it as: `assets/img/publication_preview/authorYYYYkeyword.jpg`
3. Name should match the `preview` field in your BibTeX entry

## Step 3: Add News Announcement (Optional)

Create a new file: `_news/announcement_N.md` (increment N from the last announcement)

```markdown
---
layout: post
date: YYYY-MM-DD 00:00:00-0500
inline: true
related_posts: false
---

Our research on <u>brief description of research content</u> has been published in [**<u>Journal Name</u>**](https://doi.org/10.XXXX/xxxxx).
```

### News Formatting Rules:
- Research content/title: Use `<u>underline only</u>`
- Journal name: Use `[**<u>bold + underline</u>**](journal-url)`
- Important achievements (like awards): Use `**<u>bold + underline</u>**`

### Examples:
```markdown
Our <u>first-author paper</u> "[<u>Paper Title</u>](https://url)" has been published in [**<u>Journal Name</u>**](https://doi.org/).

Our paper on <u>research topic description</u> has been published in [**<u>Journal Name</u>**](https://doi.org/).

I have been selected as a recipient of the **<u>Presidential Science Scholarship</u>** of South Korea.
```

## Step 4: Test Locally

```bash
# Using Docker (recommended)
docker compose up

# Access at http://localhost:8080
```

Check:
- Publications page shows your new paper in correct order (newest first)
- Selected Publications (if `selected=true`) appears on homepage
- Image and title are clickable and link to correct URL
- News announcement appears correctly formatted

## Step 5: Deploy

```bash
git add _bibliography/papers.bib assets/img/publication_preview/yourimage.jpg _news/announcement_N.md
git commit -m "Add publication: Brief Paper Title"
git push
```

GitHub Actions will automatically build and deploy your site in 2-5 minutes.

## Quick Checklist

- [ ] Added entry to `_bibliography/papers.bib`
- [ ] Set correct `date` field (YYYY-MM-DD) for proper sorting
- [ ] Set `selected=true` if it should appear on homepage
- [ ] Added preview image to `assets/img/publication_preview/`
- [ ] Added DOI or HTML link
- [ ] Created news announcement in `_news/`
- [ ] Used correct formatting: `<u>research content</u>` and `[**<u>Journal</u>**](url)`
- [ ] Tested locally
- [ ] Committed and pushed changes

## Notes

- Publications are automatically sorted by the `date` field (newest first)
- DOI and HTML buttons have been removed - images and titles are now clickable
- Keep image filenames consistent with BibTeX keys for easy management
- News items are displayed in reverse chronological order (newest first)
