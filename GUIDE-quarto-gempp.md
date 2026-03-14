# Guide: Building your Academic Website with Quarto + GitHub Pages

## For: René Gempp — gempp.cl
### Based on Dr. Gang He's template

---

## Site Architecture

```
Navbar:  Home | Research ▼ | Teaching ▼ | Tests & Scales | Software & Code | Professional
                 │                │
                 ├─ Publications   ├─ Courses
                 └─ Grants         ├─ Workshops
                                   └─ Tutorials
```

### Files included in this package

| File | Purpose |
|------|---------|
| `_quarto.yml` | Main site configuration (navbar, theme, footer) |
| `index.qmd` | Homepage with bio, photo, and links |
| `publications.qmd` | Auto-generated publication list from BibTeX |
| `grants.qmd` | Funded research projects (current and past) |
| `teaching-courses.qmd` | University courses (OB, Organizational Diagnosis) |
| `teaching-workshops.qmd` | Workshops and short courses |
| `teaching-tutorials.qmd` | Quarto tutorials with executable R code (listing page) |
| `tests-scales.qmd` | Psychometric instruments developed or adapted |
| `software.qmd` | Code, scripts, and tools (R, Mplus, Stata) |
| `professional.qmd` | Consulting, peer review, memberships, conferences |
| `contact.qmd` | Contact information |

---

## Part 1: Prerequisites (one-time setup)

### 1.1 Install Quarto

Download the Windows installer from: <https://quarto.org/docs/get-started/>

Run the `.msi` installer. Verify in Git Bash:

```bash
quarto --version
```

### 1.2 Verify Git

You already have Git configured (from Claude Code). Verify:

```bash
git --version
```

### 1.3 RStudio (optional but recommended)

RStudio 2022.07+ has Quarto built in. You can preview the site directly from RStudio. Not strictly required if you prefer the terminal.

---

## Part 2: Create the Repository (10 minutes)

### 2.1 Fork the template

1. Go to: <https://github.com/drganghe/quarto-academic-website-template>
2. Click **"Use this template"** → **"Create a new repository"**
3. Configure:
   - **Repository name**: `tu-username.github.io` (publishes at `https://tu-username.github.io`)
   - **Visibility**: Public (required for free GitHub Pages)
4. Click **"Create repository"**

### 2.2 Clone to your PC

```bash
cd ~/Dropbox/ANALYTICA/
git clone https://github.com/TU-USERNAME/TU-USERNAME.github.io.git
cd TU-USERNAME.github.io
```

### 2.3 Test locally

```bash
quarto preview
```

Should open the template site in your browser. `Ctrl+C` to stop.

---

## Part 3: Replace Files

### 3.1 Delete template files you won't need

```bash
rm people.qmd projects.qmd projects.yml posts.qmd
rm -rf people/ posts/
```

### 3.2 Copy the personalized files

Replace `_quarto.yml`, `index.qmd`, `publications.qmd`, and `contact.qmd` with the versions from this package. Add the new files: `grants.qmd`, `teaching-courses.qmd`, `teaching-workshops.qmd`, `teaching-tutorials.qmd`, `tests-scales.qmd`, `software.qmd`, `professional.qmd`.

### 3.3 Add your profile photo

Place your photo at `files/profiles/profile.jpg`.

### 3.4 Create your BibTeX file

1. Go to your Google Scholar profile
2. Select all publications → **Export** → **BibTeX**
3. Save as `references.bib` in the project root

Alternative: Export from Zotero as BibTeX for cleaner entries.

### 3.5 Create the tutorials folder structure

```bash
mkdir -p teaching/tutorials
```

When you create your first tutorial, add a subfolder:

```
teaching/tutorials/intro-irt/
└── index.qmd
```

### 3.6 Replace placeholders

Search all `.qmd` files for these strings and replace them:

- `TU-USERNAME` → your GitHub username
- `TU-ID` → your Google Scholar user ID
- `TU-ORCID` → your ORCID (uncomment lines when ready)

---

## Part 4: Render and Publish

### 4.1 Render locally

```bash
quarto render
```

### 4.2 Preview

```bash
quarto preview
```

### 4.3 Push to GitHub

```bash
git add .
git commit -m "Initial personalized site"
git push
```

### 4.4 Configure GitHub Pages

1. Go to your repository on GitHub
2. **Settings** → **Pages**
3. **Source**: "Deploy from a branch"
4. **Branch**: `main`, folder `/docs`
5. Click **Save**

Wait 2-5 minutes. Your site will be live.

---

## Part 5: Connect gempp.cl

### 5.1 In GitHub

**Settings** → **Pages** → **Custom domain** → type `gempp.cl` → **Save**

### 5.2 At your domain registrar

Add these DNS records:

**For gempp.cl (apex domain):**

| Type | Host | Value |
|------|------|-------|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |

**For www.gempp.cl:**

| Type | Host | Value |
|------|------|-------|
| CNAME | www | tu-username.github.io |

### 5.3 Enable HTTPS

Once DNS propagates (up to 48h), go to **Settings** → **Pages** → check **"Enforce HTTPS"**.

---

## Part 6: Adding Content Over Time

### Adding a new tutorial (with R code)

1. Create `teaching/tutorials/my-tutorial/index.qmd`
2. Write your tutorial with executable R chunks
3. `quarto render` and push

Example `index.qmd` header:

```yaml
---
title: "Introduction to IRT with mirt"
description: "A practical walkthrough of Rasch and GRM models in R"
date: 2026-04-01
categories: [IRT, R, psychometrics]
execute:
  echo: true
---
```

### Adding a dedicated course page

Create a subfolder like `teaching/ob-2026/` with its own `index.qmd`. Link to it from `teaching-courses.qmd`. The course page can include syllabus, slides (Reveal.js), assignments, and R-based materials.

### Adding a psychometric report for a test

Create a subfolder like `tests/bmslss/index.qmd` with the full psychometric documentation. Link to it from `tests-scales.qmd`.

---

## Part 7: Regular Workflow

Once the site is running:

1. Edit `.qmd` files in your editor (RStudio, VS Code)
2. `quarto preview` to check changes
3. `quarto render` to build the final site
4. `git add . && git commit -m "description" && git push`
5. GitHub Pages updates automatically (1-2 minutes)

---

## Useful Resources

- Quarto documentation: <https://quarto.org/docs/websites/>
- Gang He's academic site tips: <https://drganghe.github.io/quarto-academic-site-examples.html>
- Publishing to GitHub Pages: <https://quarto.org/docs/publishing/github-pages.html>
- Andrew Heiss's site (reference): <https://www.andrewheiss.com/>
- Hugo → Quarto migration (Spanish): <https://jc-castillo.com/blog/posts/quarto-migration/>
- qtwAcademic R package: <https://github.com/andreaczhang/qtwAcademic>
