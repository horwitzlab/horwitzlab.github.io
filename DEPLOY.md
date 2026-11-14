# Horwitz Lab Website — GitHub Pages Deployment

## One-time setup (takes about 10 minutes)

### 1. Create a GitHub account (if you don't have one)

Go to https://github.com and sign up. A free account is all you need.

### 2. Create a new repository

1. Go to https://github.com/new
2. Name it `horwitzlab.github.io` (using your GitHub username instead of "horwitzlab" if different — but `horwitzlab.github.io` gives you the cleaner URL `https://horwitzlab.github.io/`)
3. Set it to **Public**
4. Leave everything else unchecked and click **Create repository**

### 3. Install Git (if not already installed)

- **Mac:** Open Terminal and run `git --version`. If it's not installed, macOS will prompt you to install Xcode Command Line Tools.
- **Windows:** Download from https://git-scm.com/download/win

### 4. Push the site to GitHub

Open Terminal (Mac) or Git Bash (Windows) and run these commands one at a time:

```bash
cd /path/to/horwitzlab          # navigate to the unzipped folder
git init
git add .
git commit -m "Initial site"
git branch -M main
git remote add origin https://github.com/horwitzlab/horwitzlab.github.io.git
git push -u origin main
```

Replace `horwitzlab` in the remote URL with your actual GitHub username.

### 5. Enable GitHub Pages

1. In your repository on GitHub, click **Settings** (top tab)
2. Click **Pages** in the left sidebar
3. Under **Source**, select **GitHub Actions**
4. Click **Save**

GitHub will now automatically run the build workflow whenever you push changes. The first build takes about 2 minutes. After that, your site will be live at **https://horwitzlab.github.io/** (or whatever your repository name is).

---

## Making changes later

The site is designed so that most updates can be made by editing plain text files — no coding required.

### Adding or updating a lab member

Edit `data/members.yaml`. Each entry looks like this:

```yaml
- name: Jane Smith
  role: Graduate Student
  photo: /images/jane-smith.jpg   # optional; see Photos section below
  bio: >
    Jane joined the lab in 2024 and studies ...
  links:
    - label: UW Profile
      url: https://...
```

### Adding a publication

Edit `data/publications.yaml`. Add a new entry in the right year block:

```yaml
- year: '2027'
  papers:
    - authors: Smith J, Jones B, and Horwitz GD, 2027
      title: A new paper title.
      journal: Journal of Neuroscience
      url: https://drive.google.com/...   # Google Drive link to PDF
```

### Adding links

Edit `data/links.yaml`.

### Editing the research description

Edit `content/research/index.md` — it's plain Markdown.

### After any edit

```bash
git add .
git commit -m "Update members"   # or whatever you changed
git push
```

GitHub automatically rebuilds and deploys the site. Changes go live in about 90 seconds.

---

## Adding member photos

Photos are not included in the zip because they weren't in the WordPress export.

1. Download the photos you want from the old WordPress site (right-click → Save Image)
2. Put them in the `static/images/` folder inside the site directory
3. Update `data/members.yaml` to point to `/images/filename.jpg`
4. Push the changes

---

## Pointing depts.washington.edu/horwitzlab to the new site

Once the GitHub Pages site is working, you can ask UWIT to set up a redirect from your old URL. Send them a request saying:

> "I'd like to redirect depts.washington.edu/horwitzlab to https://horwitzlab.github.io/. Please set up a 301 redirect from the old URL to the new one."

UWIT can typically do this within a few days. Until then, both URLs work — the old WordPress site at the original URL and the new static site at the GitHub Pages URL.

---

## Site structure

```
horwitzlab/
├── hugo.yaml                   # site config (title, URLs, nav menu)
├── content/                    # one stub file per page
│   ├── _index.md               # homepage
│   ├── research/index.md       # research page content
│   ├── members/index.md
│   ├── publications/index.md
│   ├── gallery/index.md
│   └── links/index.md
├── data/                       # structured data (edit these for updates)
│   ├── members.yaml
│   ├── publications.yaml
│   └── links.yaml
├── themes/horwitz/
│   ├── layouts/                # HTML templates
│   ├── static/css/main.css     # all styling
│   └── static/favicon.svg
└── .github/workflows/deploy.yml  # auto-deploy on push
```
