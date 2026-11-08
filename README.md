# Bridgetown App Studio website

This repository hosts the public Bridgetown App Studio website at
[https://bridgetownappstudio.com](https://bridgetownappstudio.com).

## Architecture and hosting

The site is a static website built from `index.html` and the assets stored in this
repository. It uses the legacy GitHub Pages deployment model: GitHub Pages
publishes the repository root from the `main` branch. The `CNAME` file configures
the custom domain `bridgetownappstudio.com`, and HTTPS is enforced for the live
site.

## Prerequisites

- Git
- GitHub access to this repository
- Python 3, or an equivalent simple static-file server, for local preview

## Development workflow

Start from an up-to-date `main` branch and make each change on a focused branch:

```sh
git switch main
git pull --ff-only origin main
git switch -c your-focused-branch
```

Edit `index.html` or the relevant assets, then preview the repository root
locally:

```sh
python3 -m http.server 8000
```

Visit [http://localhost:8000](http://localhost:8000) and check the site at
desktop and mobile widths. Test navigation, external links, images, and other
assets. When finished, stop the server with <kbd>Control</kbd>+<kbd>C</kbd>.

Before committing, inspect the exact changes:

```sh
git status --short
git diff
```

Commit the focused change, push the branch, and open a pull request:

```sh
git add <changed-files>
git commit -m "Describe the website change"
git push -u origin your-focused-branch
```

Review the pull request and merge it into `main` after the checks pass. Opening a
pull request is the normal workflow; do not push directly to `main`.

## Homepage and Dove product page

The studio homepage (`index.html`) introduces Dove and its maker. The consumer
product page lives at `/dove/` (`dove/index.html`); both share `assets/site.css`.
They link to the same App Store listing, with current local subscription pricing
and terms left to the App Store and purchase screen. Saving and exploring are
free; creating Plans requires Dove Plus, while invitees can join and vote without
subscribing.

The JPEGs in `dove/assets/` are smaller display copies of the existing press
artwork: `dining.jpg` comes from `generated-couple.png`, and
`choose-together.jpg` comes from `Dove-Search-v3.png`. Keep the original mark
unchanged and retain the captions identifying generated imagery and illustrative
UI. Original press downloads remain in `dove/press/`.

## Dove press room

The press room lives at `/dove/press/` and follows the static HTML/CSS workflow
above. Its downloadable press release and fact sheet have editable HTML sources
beside their PDFs in `dove/press/downloads/`. After editing either HTML file or
`documents.css`, open the HTML in a browser and print to PDF using its CSS page
size, background graphics enabled, and browser headers/footers disabled. Check
that each PDF remains one page, contains the launch date and working download
link, and has no clipped text.

When replacing artwork, keep the displayed image, individual download, version
labels, fact sheet, `ARTWORK-USAGE.txt`, and artwork ZIP consistent. The ZIP
contains only the logo, header artwork, Search artwork, and usage notes. Keep
internal outreach and review documents out of public downloads.

## Deployment

GitHub Pages automatically publishes the repository root after a pull request is
merged into `main`. No separate build or deployment command is required.

After merging:

1. Open the repository on GitHub and check **Settings > Pages** for the current
   deployment status and custom-domain configuration.
2. If the repository exposes a Pages deployment or workflow status, confirm that
   the latest deployment completed successfully.
3. Visit [https://bridgetownappstudio.com](https://bridgetownappstudio.com) and
   verify the change in production.

Publishing, DNS propagation, and browser or CDN caches can take a few minutes to
settle.

## Custom-domain safety

Keep `CNAME` in the repository root with exactly this domain:

```text
bridgetownappstudio.com
```

Do not delete or casually edit `CNAME`, change the GitHub Pages custom-domain
setting, or alter the domain's DNS records. These settings work together, and an
uncoordinated change can make the site unavailable or break HTTPS.

## Rollback

If a merged change causes a problem, create a new branch from the latest `main`,
revert the problematic commit, and open a follow-up pull request:

```sh
git switch main
git pull --ff-only origin main
git switch -c revert-problematic-change
git revert <problematic-commit>
git push -u origin revert-problematic-change
```

After the revert pull request is reviewed and merged, confirm that GitHub Pages
rebuilds successfully and verify the live site again.

## Troubleshooting

- **The live site looks stale:** Wait a few minutes, then hard-refresh the page
  or test in a private browsing window to bypass local cache.
- **A change is not deployed:** Check **Settings > Pages** and any Pages
  deployment status for errors, and confirm that the change reached `main`.
- **An asset works locally but not in production:** Check the path's exact
  capitalization. GitHub Pages paths are case-sensitive.
- **Images, styles, or links are broken:** Check relative asset paths from the
  page that references them, including directory depth and filename extensions.
- **The custom domain stops working:** Confirm that the root `CNAME` file still
  exists and contains only `bridgetownappstudio.com`. Coordinate any DNS or Pages
  setting changes before making them.

## Pre-merge checklist

- [ ] The branch started from the latest `main`.
- [ ] The change is focused, and `git diff` contains only intended files.
- [ ] The site was previewed locally at desktop and mobile widths.
- [ ] Navigation, external links, and asset paths were tested.
- [ ] `CNAME` still contains `bridgetownappstudio.com`.
- [ ] `git diff --check` passes.
- [ ] The pull request clearly describes the change and its verification.
