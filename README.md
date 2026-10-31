# Personal website

The home page contains Lorenzo Balandi’s portrait, introduction, and real LinkedIn, GitHub, and YouTube links. The CV page presents research and work experience, education, and training as vertical timelines. PhD Thesis contains the supplied abstract; Personal projects remains work in progress. These edits are local; this workflow does not push or publish them.

## Files and local preview

- `index.html`: home page, name, portrait, introduction, and profile links.
- `cv.html`: research and work experience, education, and training timelines.
- `thesis.html`: PhD Thesis abstract.
- `projects.html`: work-in-progress page.
- `assets/P1033650.JPG`: the supplied portrait.
- `assets/website_intro.mp4`: retained for future editing; currently not displayed or loaded by the website.
- `text/intro.txt` and `text/thesis.txt`: source text for the introduction and abstract. Their content is copied into HTML; changing the text files alone will not update the website.
- `styles.css`: layout, typography, and colors.
- `.nojekyll`: serves the files directly on GitHub Pages.
- `DESIGN.md`: brief design notes.
- `preview.png`: local screenshot, excluded from Git by `.gitignore`.

Open `index.html` directly in a browser. Alternatively, from the project directory run:

```sh
python3 -m http.server 8000 --bind 127.0.0.1
```

Visit http://127.0.0.1:8000 and stop the server with Ctrl+C. No build step or dependencies are needed.

## Update the content

Edit `index.html` for the introduction and profile links, `cv.html` for timeline entries, and `thesis.html` for the abstract. Text from `text/intro.txt` and `text/thesis.txt` has been copied into HTML to support opening the site directly as local files; keep those copies in sync after edits. The CV is based on the supplied October 2026 document; completion dates marked as expected are not completed degrees.

Each timeline marker uses plain initials, not an official institution logo. Logo permission for personal-site use was not established. Relevant guidance: [Inria](https://jobs.inria.fr/public/en/mentions-legales), [NYU](https://guides.nyu.edu/copyright/nyupermissions), and [University of Bologna](https://www.unibo.it/en/university/statute-standards-strategies-and-reports/image-identity-brand/university-seal). Approved logo assets can replace the markers later.

The pages share the same top navigation and stylesheet. If you change navigation labels or add pages, update all four HTML files. Relative paths allow local file previews and GitHub Pages hosting.

## Push to GitHub and publish this website

The local repository is already initialized on branch `main` with this remote:

- Repository: https://github.com/lorenzo-balandi/lorenzo-balandi.github.io
- Remote `origin`: `https://github.com/lorenzo-balandi/lorenzo-balandi.github.io.git`
- Website address after publishing: https://lorenzo-balandi.github.io/

Do not run `git init`, create another repository, or add another `origin`. The account name `lorenzo-balandi` matches the repository name `lorenzo-balandi.github.io`, which is the required naming pattern for an account or organization Pages site. No purchased domain or DNS configuration is needed.

### 1. Authenticate with GitHub

Open a terminal. If GitHub CLI is already configured, check its login:

```sh
gh auth status
```

If not signed in, run:

```sh
gh auth login
```

Choose **GitHub.com**, **HTTPS**, **Yes** when asked to authenticate Git, and **Login with a web browser**. Complete the browser login using your personal GitHub account that has write access to the organization repository. Then run:

```sh
gh auth setup-git
```

If `gh` is not installed, follow the [official installation instructions](https://github.com/cli/cli#installation). On Ubuntu/Debian with the package available in your configured repositories, you can install it with `sudo apt update` followed by `sudo apt install gh`.

These commands configure GitHub authentication; they do not replace GitLab credentials. GitHub does not accept your account password for HTTPS Git pushes. An existing SSH or credential-manager setup can be used instead of GitHub CLI.

See [GitHub authentication instructions](https://docs.github.com/en/get-started/git-basics/caching-your-github-credentials-in-git).

### 2. Commit and push the current website

Run these commands from your terminal:

```sh
cd /home/lorenzo/personal_website
git status --short --branch
git remote -v
git add index.html cv.html thesis.html projects.html styles.css assets/P1033650.JPG text/intro.txt text/thesis.txt .nojekyll .gitignore README.md DESIGN.md
git diff --cached --stat
git commit -m "Update personal website with CV and thesis"
git push origin main
```

The explicit file list includes the website pages, portrait, source text, and documentation. It leaves the unused video local for future editing and excludes the preview screenshot. After pushing, confirm that `cv.html`, `thesis.html`, `projects.html`, `styles.css`, and `assets/P1033650.JPG` appear in the GitHub repository.

If Git reports an unknown author identity, set your desired author name and email for this repository, then retry the commit. Use an email associated with your GitHub account or its GitHub-provided noreply address:

```sh
git config user.name "Lorenzo Balandi"
git config user.email "YOUR_CHOSEN_COMMIT_EMAIL"
```

If the push is rejected because the remote has newer commits, run `git pull --rebase origin main`, resolve any conflicts if prompted, and push again. Do not force-push. If your working tree has other uncommitted changes, commit or stash those intentionally before rebasing.

### 3. Enable public GitHub Pages hosting

1. Open [the repository](https://github.com/lorenzo-balandi/lorenzo-balandi.github.io).
2. If it is private and the organization uses **GitHub Free**, change it to **Public** under **Settings → General → Danger Zone → Change repository visibility**. Public visibility includes committed source and history. If it is already public, skip this step. Eligible paid plans can host Pages from private repositories.
3. Open **Settings → Pages**.
4. Under **Build and deployment**, set **Source** to **Deploy from a branch**.
5. Select branch **main** and folder **/(root)**, then click **Save**.
6. Leave **Custom domain** empty.
7. Check **Actions** for the Pages build and deployment result. Once it succeeds, Pages settings should show the published address.
8. Visit https://lorenzo-balandi.github.io/ and check Home, CV, PhD Thesis, and Personal projects, as well as the portrait and profile links.

The site can take up to 10 minutes to publish after a push. There is no build command to run locally: these are plain HTML and CSS files, and `.nojekyll` disables Jekyll processing.

Official guidance: [Pages publishing settings](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site) and [creating a Pages site](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site).

### 4. Publish future updates

Before starting edits, pull changes made elsewhere:

```sh
cd /home/lorenzo/personal_website
git pull --ff-only origin main
```

Edit and preview locally. Then stage the files you changed, review the staged summary, commit, and push:

```sh
git add index.html cv.html thesis.html projects.html styles.css assets/P1033650.JPG text/intro.txt text/thesis.txt README.md DESIGN.md
git diff --cached --stat
git commit -m "Update website content"
git push origin main
```

Add other intended assets to the staging command when introduced. Once Pages is configured, each push to `main` redeploys the public website automatically. Check **Actions** if an update does not appear; after a successful deployment, refresh the browser.
