# Academic Pages
**Academic Pages is a Github Pages template for academic websites.**

ADAPTED VERSION - KEY CHANGES INCLUDE 

## Customized from Academic Pages Template

Baseline used for comparison: initial import commit on `2025-01-25` (`e5ced30`), then all template-level differences tracked up to current `master`.

### 1) Typography and visual system
- Replaced template font stack with Google Fonts, primarily **Poppins** (`/_includes/head.html`, `/_sass/_variables.scss`).
- Added Google Fonts stylesheet import in head for `Poppins` and `Lato` (`/_includes/head.html`).
- Reduced base doc font size (`16` -> `15`) and tuned type scale sizes (`/_sass/_variables.scss`).
- Set global/header/caption font families to Poppins (`/_sass/_variables.scss`).
- Increased right sidebar widths for content breathing room (`/_sass/_variables.scss`).

### 2) Color palette and link behavior
- Introduced custom palette variables:
  - `bright-orange` (`#FF9F1C`)
  - `vibrant-red` (`#E71D36`)
  - `teal` (`#2EC4B6`)
  - `dark-navy` (`#011627`)
  - `off-white` (`#FDFFFC`)
  (`/_sass/_variables.scss`)
- Overrode link colors to orange/red pair and masthead colors to navy/teal (`/_sass/_variables.scss`).
- Added explicit underline + hover color behavior to links (`/_sass/_base.scss`).
- Recolored navigation accents, borders, hover states, and archive taxonomy separators using custom palette (`/_sass/_navigation.scss`).

### 3) Header, favicon, and branding details
- Added custom favicon references (`favicon-slug.ico`, `images/samslug.png`) in head include (`/_includes/head.html`).
- Added custom favicon assets in repo root and images (`/favicon-slug.ico`, `/favicon.ico`, `/images/samslug.png`).

### 4) Layout-level template changes
- Removed site footer block from default layout (`/_layouts/default.html`).
- Deleted stock footer include entirely (`/_includes/footer.html`).
- Cleared custom footer snippet content (`/_includes/footer/custom.html`).
- Added `hide_title` support in archive layout to optionally suppress page title rendering (`/_layouts/archive.html`).
- Reworked single-page publication presentation with dedicated title/description/download sections (`/_layouts/single.html`).

### 5) Publications/archive component redesign
- Replaced stock `archive-single` behavior with simplified item cards (`/_includes/archive-single.html`):
  - no teaser thumbnail rendering
  - no permalink icon/read-time block
  - non-clickable title text
  - excerpt shown as styled description block
  - download links shown in a compact action row
- Added archive styles for:
  - tighter title sizing/weight
  - styled description text
  - reusable action link row
  - full-width list alignment with reduced side padding
  (`/_sass/_archive.scss`)

### 6) Gallery system customization
- Expanded gallery include to support `gallery=` input directly (in addition to page-scoped gallery IDs) (`/_includes/gallery`).
- Added metadata-aware rendering mode:
  - auto-switches to grid card layout when any item has `title`/`caption`
  - outputs `figure/figcaption` per image with title/caption blocks
  (`/_includes/gallery`)
- Added support for absolute image paths beginning with `/` (important for reusable galleries and data galleries) (`/_includes/gallery`).
- Preserved fallback legacy rendering for image-only galleries (`/_includes/gallery`).
- Introduced structured data gallery source file (`/_data/data_gallery.yml`) with section titles/descriptions and item metadata.
- Added gallery-specific style system (`/_sass/_page.scss`):
  - `.gallery--grid`, `.gallery__item`, `.gallery__title`, `.gallery__caption`
  - `.data-gallery` responsive sizing rules
  - `.about-gallery` horizontal strip behavior
  - placeholder/description helper styles

### 7) Navigation and information architecture changes
- Renamed top-level nav labels (`/_data/navigation.yml`):
  - `Publications` -> `Research`
  - `Talks` -> `Public opinion`
  - `Teaching` -> `Learning`
- Added new `Data` tab and page (`/_data/navigation.yml`, `/_pages/data.html`).
- Disabled several default template links (Portfolio, Blog Posts, CV, Guide) in nav (`/_data/navigation.yml`).
- Replaced stock About page flow with homepage-first profile page (`/_pages/index.md`) and about redirects.

### 8) Page-level component styling additions
- Added custom teaching section styles and link-row layout for resource blocks (`/_sass/_page.scss`).
- Added `home-intro` sizing for homepage intro paragraphs (`/_sass/_page.scss`).
- Reduced hero title size for a cleaner archive/single heading scale (`/_sass/_page.scss`).
- Updated sidebar portrait treatment:
  - circular -> square image
  - updated border/padding
  - larger sidebar body text
  (`/_sass/_sidebar.scss`)

### 9) Template configuration behavior changes
- Updated publication category groups and labels to project-specific taxonomy (`/_config.yml`).
- Enabled read-more behavior for excerpts (`read_more: "enabled"`) (`/_config.yml`).
- Updated repository/site metadata and sidebar author profile defaults to project values (`/_config.yml`).



![Academic Pages template example](images/homepage.png "Academic Pages template example")

# Getting Started

1. Register a GitHub account if you don't have one and confirm your e-mail (required!)
1. Click the "Use this template" button in the top right.
1. On the "New repository" page, enter your repository name as "[your GitHub username].github.io", which will also be your website's URL.
1. Set site-wide configuration and add your content.
1. Upload any files (like PDFs, .zip files, etc.) to the `files/` directory. They will appear at https://[your GitHub username].github.io/files/example.pdf.
1. Check status by going to the repository settings, in the "GitHub pages" section
1. (Optional) Use the Jupyter notebooks or python scripts in the `markdown_generator` folder to generate markdown files for publications and talks from a TSV file.

See more info at https://academicpages.github.io/

## Running locally

When you are initially working your website, it is very useful to be able to preview the changes locally before pushing them to GitHub. To work locally you will need to:

1. Clone the repository and made updates as detailed above.
1. Make sure you have ruby-dev, bundler, and nodejs installed
    
    On most Linux distribution and [Windows Subsystem Linux](https://learn.microsoft.com/en-us/windows/wsl/about) the command is:
    ```bash
    sudo apt install ruby-dev ruby-bundler nodejs
    ```
    On MacOS the commands are:
    ```bash
    brew install ruby
    brew install node
    gem install bundler
    ```
1. Run `bundle install` to install ruby dependencies. If you get errors, delete Gemfile.lock and try again.
1. Run `jekyll serve -l -H localhost` to generate the HTML and serve it from `localhost:4000` the local server will automatically rebuild and refresh the pages on change.

If you are running on Linux it may be necessary to install some additional dependencies prior to being able to run locally: `sudo apt install build-essential gcc make`

## Using Docker

Working from a different OS, or just want to avoid installing dependencies? You can use the provided `Dockerfile` to build a container that will run the site for you if you have [Docker](https://www.docker.com/) installed.

Start by build the container:

```bash
docker build -t jekyll-site .
```

Next, run the container:
```bash
docker run -p 4000:4000 --rm -v $(pwd):/usr/src/app jekyll-site
```

To run the `docker run` command on Windows, you need to adjust the syntax for the volume mapping (`-v`) as Windows uses different path formats. Here's how to run your command on Windows:

### Steps for Windows:
1. **Check Docker Installation**: Ensure Docker is installed and running.
2. **Adjust Path for Volume Mapping**:

   - On Windows, replace `$(pwd)` with the full absolute path to your current directory. For example:

     ```bash
     -v C:\path\to\your\site:/usr/src/app
     ```

### Full Command Example:
```bash
docker run -p 4000:4000 --rm -v C:\path\to\your\site:/usr/src/app jekyll-site
```

### Things to Keep in Mind:
1. **Use PowerShell**:
   - If you are using PowerShell, you can use `${PWD}` for the current directory:
     ```bash
     docker run -p 4000:4000 --rm -v ${PWD}:/usr/src/app jekyll-site
     ```

2. **Enable Docker File Sharing**:
   - If your volume doesn't map correctly, ensure Docker has access to the drive where your project resides. To do this:
     - Open Docker Desktop.
     - Go to *Settings* → *Resources* → *File Sharing*.
     - Add your drive (e.g., `C:`).

3. **Run in Command Prompt or PowerShell**:
   - In *Command Prompt*:
   
     ```bash
     docker run -p 4000:4000 --rm -v C:\path\to\your\site:/usr/src/app jekyll-site
     ```
   - In *PowerShell*:

     ```bash
     docker run -p 4000:4000 --rm -v ${PWD}:/usr/src/app jekyll-site
     ```

# Maintenance

Bug reports and feature requests to the template should be [submitted via GitHub](https://github.com/academicpages/academicpages.github.io/issues/new/choose). For questions concerning how to style the template, please feel free to start a [new discussion on GitHub](https://github.com/academicpages/academicpages.github.io/discussions).

This repository was forked (then detached) by [Stuart Geiger](https://github.com/staeiou) from the [Minimal Mistakes Jekyll Theme](https://mmistakes.github.io/minimal-mistakes/), which is © 2016 Michael Rose and released under the MIT License (see LICENSE.md). It is currently being maintained by [Robert Zupko](https://github.com/rjzupkoii) and additional maintainers would be welcomed.

## Bugfixes and enhancements

If you have bugfixes and enhancements that you would like to submit as a pull request, you will need to [fork](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo) this repository as opposed to using it as a template. This will also allow you to [synchronize your copy](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/syncing-a-fork) of template to your fork as well.

Unfortunately, one logistical issue with a template theme like Academic Pages that makes it a little tricky to get bug fixes and updates to the core theme. If you use this template and customize it, you will probably get merge conflicts if you attempt to synchronize. If you want to save your various .yml configuration files and markdown files, you can delete the repository and fork it again. Or you can manually patch.

---
<div align="center">
    
![pages-build-deployment](https://github.com/academicpages/academicpages.github.io/actions/workflows/pages/pages-build-deployment/badge.svg)
[![GitHub contributors](https://img.shields.io/github/contributors/academicpages/academicpages.github.io.svg)](https://github.com/academicpages/academicpages.github.io/graphs/contributors)
[![GitHub release](https://img.shields.io/github/v/release/academicpages/academicpages.github.io)](https://github.com/academicpages/academicpages.github.io/releases/latest)
[![GitHub license](https://img.shields.io/github/license/academicpages/academicpages.github.io?color=blue)](https://github.com/academicpages/academicpages.github.io/blob/master/LICENSE)

[![GitHub stars](https://img.shields.io/github/stars/academicpages/academicpages.github.io)](https://github.com/academicpages/academicpages.github.io)
[![GitHub forks](https://img.shields.io/github/forks/academicpages/academicpages.github.io)](https://github.com/academicpages/academicpages.github.io/fork)
</div>
