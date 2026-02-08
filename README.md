# Luke Anglin Portfolio

Personal website for Luke Anglin, hosted on GitHub Pages.

## Usage

1.  **Edit Content**: Modify `index.html`.
2.  **Edit Styles**: Modify `styles.css`.
3.  **Publish**: Push to `main`.

**Resume**: Update the link in `index.html` with your direct OneDrive download link.

## Running Locally

To preview the site locally:

1.  **Open directly**: You can simply double-click `index.html` to open it in your browser.
2.  **Using Python (Recommended)**:
    Run the following command in the terminal from the project directory:
    # Luke Anglin — Portfolio (static)

    This repository contains a small static portfolio website intended for GitHub Pages.

    ## Overview

    - Type: Static HTML/CSS site (single-page portfolio).
    - Main entry: [index.html](index.html)
    - Styles: [styles.css](styles.css)
    - Assets: `assets/` (images, resume PDF)
    - Legacy Jekyll site: `_legacy_backup/` (archived Jekyll layout, posts, and Gemfile)

    ## Quick Local Preview

    You can preview the site locally from the project root.

    Open directly in your browser (double-click `index.html`), or run a simple HTTP server:

    ```bash
    python3 -m http.server 8000
    # then visit http://localhost:8000
    ```

    ## Deploy (GitHub Pages)

    - Push the repository to your GitHub account and enable GitHub Pages for the `main` branch (root) in repository settings.
    - Alternatively deploy from a `gh-pages` branch or use GitHub Actions if you prefer CI-based deploys.

    ## Notes & Actionable Items

    - Contact form in [index.html](index.html) uses a Formspree placeholder `YOUR_FORM_ID`. Replace that with your actual Formspree form ID or replace with another contact method.
    - Resume link in [index.html](index.html) points to `assets/Luke_Anglin_Resume.pdf`. Confirm the file exists in `assets/` or update the link to the hosted/OneDrive URL you want to use.
    - Fonts and icons are loaded from external CDNs (Google Fonts and FontAwesome). No build step is required.

    ## Quick checks

    Verify assets and important strings quickly:

    ```bash
    ls -la assets
    grep -n "YOUR_FORM_ID" -R || true
    ```

    ## Cleanup / Notes about `_legacy_backup`

    `_legacy_backup/` contains a prior Jekyll-based version of the site (layouts, `_posts`, Gemfile). It is an archive and not used by the current static site unless you choose to restore a Jekyll workflow.

    If you'd like, I can:
    - update the Formspree ID in `index.html` (you provide the ID),
    - verify that `assets/Luke_Anglin_Resume.pdf` and `assets/images/profile.jpg` exist and fix links, or
    - remove/relocate `_legacy_backup/` (if you want a smaller repo).

    ---
    Updated: January 17, 2026
