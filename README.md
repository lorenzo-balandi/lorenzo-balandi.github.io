# Personal website

The page currently displays only “Lorenzo” and “work in progress”. It is saved locally. No repository has been created online and nothing has been published.

## Files and local preview

- `index.html`: visible content, browser title, and page description.
- `styles.css`: layout, typography, and colors.
- `.nojekyll`: serves the files directly on GitHub Pages.
- `DESIGN.md`: brief design notes.
- `preview.png`: local screenshot, excluded from Git by `.gitignore`.

Open `index.html` directly in a browser. Alternatively, from the project directory run:

```sh
python3 -m http.server 8000 --bind 127.0.0.1
```

Visit http://127.0.0.1:8000 and stop the server with Ctrl+C. No build step or dependencies are needed.

## The intended address: customname.github.io

To use `https://customname.github.io` while keeping your existing personal GitHub username, create a GitHub **organization whose account name is `customname`**, then create a repository **inside that organization** named `customname.github.io`.

`customname` is an example: replace it throughout these instructions with an available organization account name you choose. Use the organization's actual account name, not just its display name.

You administer the organization through your existing personal GitHub account. You do not need to buy a domain or configure DNS. Leave the Pages **Custom domain** setting empty: `customname.github.io` is a GitHub-provided address, not a separately registered custom domain.

The website URL will use the organization name. This does not make your GitHub identity anonymous; your account can still be associated with the organization or repository.

### Why the repository name matters

| Site type | Repository location | Default website address |
| --- | --- | --- |
| Personal account site | `YOUR_USERNAME/YOUR_USERNAME.github.io` | `https://YOUR_USERNAME.github.io` |
| Organization site — the intended setup | `customname/customname.github.io` | `https://customname.github.io` |
| Project site | `YOUR_USERNAME/personal-website` | `https://YOUR_USERNAME.github.io/personal-website/` |

An arbitrary repository name creates a project site; it does not let you choose the text before `.github.io`. Naming a repository `customname.github.io` under your personal account also does not reserve that address. The owner account must match.

Source: [GitHub Pages site types](https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages).

## One workflow: develop privately, publish when ready

### 1. Create the organization and a private repository

1. Sign in to your existing GitHub account.
2. Open your account's **Settings → Organizations → New organization**.
3. Choose the free plan and an available organization account name, represented here by `customname`.
4. Create a repository with the organization selected as **Owner**, named exactly `customname.github.io`.
5. Choose **Private** while developing. Leave initialization with README, license, and `.gitignore` off because the files already exist locally.
6. Leave Pages unconfigured until you are ready to publish.

See [creating an organization](https://docs.github.com/en/organizations/collaborating-with-groups-in-organizations/creating-a-new-organization-from-scratch).

### 2. Upload the local files once

With Git installed, run these commands from your project directory. Replace `customname` in the remote URL with the organization name you chose:

```sh
git init -b main
git add index.html styles.css .nojekyll .gitignore README.md DESIGN.md
git commit -m "Create minimal personal website"
git remote add origin https://github.com/customname/customname.github.io.git
git push -u origin main
```

If this folder is already a Git repository, skip `git init`. If the files are already committed, skip the initial add and commit. Use the existing branch name if it differs from `main`. If `origin` already exists, inspect `git remote -v` before configuring a remote; do not initialize a second repository.

Authenticate using a credential manager, GitHub CLI sign-in, a personal access token, or a configured SSH key. An HTTPS Git operation does not accept your GitHub account password.

Pushing to this private repository saves your source and version history online. It does not publish the website while Pages remains unconfigured.

### 3. Continue working privately

Before editing, pull any changes made from another computer or the GitHub interface:

```sh
git pull --ff-only origin main
```

Edit and preview locally, then save changes online:

```sh
git add index.html styles.css README.md DESIGN.md
git commit -m "Update personal website"
git push origin main
```

Add other intended files to the staging command when you introduce them.

### 4. Publish the same repository when ready

1. With the free organization plan, change this repository to **Public** under **Settings → General → Danger Zone → Change repository visibility**. This also makes its committed history public.
2. Open **Settings → Pages**.
3. Under **Build and deployment**, select **Deploy from a branch**.
4. Choose **main** (or your actual branch), select **/(root)**, and click **Save**.
5. Leave **Custom domain** empty.
6. Check the **Actions** tab for the deployment result. Pages settings will show the final address: `https://customname.github.io`.

Subsequent pushes to the publishing branch update the public website automatically. No second upload or new Git repository is needed.

GitHub Free supports Pages from public repositories. Eligible paid plans also support Pages from private repositories, but ordinary Pages hosting is still public. See [Pages publishing settings and plan requirements](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).

## Is GitLab needed?

No. A private GitLab repository is an alternative place to store unfinished work, not a prerequisite for publishing on GitHub. Using it first would introduce a second hosting service and a later move or additional remote.

The workflow above uses one private GitHub repository, local editing, and then publication from that same repository. If you prefer GitLab, you can store the source in a private GitLab project and continue previewing locally. GitLab also offers authenticated Pages previews through [Pages access control](https://docs.gitlab.com/user/project/pages/pages_access_control/).
