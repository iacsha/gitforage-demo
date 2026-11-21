# gitforage field guide (beta)

The public field guide of [gitforage](https://github.com/iacsha/gitforage), live at **https://gitforage.dev**. Each week it forages GitHub across five patches: healthcare interoperability, self-hosting and homelab, home automation, developer tools, and AI coding agents. Pick your patch on the site to re-rank the finds to your own topics, and Keep or Skip any card to help tune it.

Want a guide of your own? Follow the setup below.

---

# My gitforage portal

This repo runs [gitforage](https://github.com/iacsha/gitforage). Once a week it searches GitHub for projects that fit the interests in `interests.yml`, ranks them by fit with a reason for every point, and publishes them as a small website on GitHub Pages, with an Atom feed. Keep and Skip buttons on each card teach it what you like.

## Set it up (about five minutes)

1. **Pin gitforage.** Open `.github/workflows/forage.yml` and `.github/workflows/feedback.yml`. Near the top, `GITFORAGE_SHA` names the gitforage commit this portal runs. If it is all zeros, set both to the commit you want to run. The workflows refuse to run until it is set.
2. **Describe your interests.** Edit `interests.yml`: a few GitHub topics, some projects you follow (`seeds`), and ideally your GitHub username in `stars_from`. Every key is commented.
3. **Turn on Pages.** Settings, Pages, and under "Build and deployment" set Source to **GitHub Actions**.
4. **Run it once.** Actions, **forage**, Run workflow. It takes a few minutes. Your portal is then at `https://<your-username>.github.io/<this-repo>/`.
5. **Optional: a label.** Issues, Labels, New label: `gitforage-feedback`. Feedback issues get it automatically once it exists. The workflow finds them by title even without it.

That's it. The forage workflow runs every Sunday at 06:17 UTC. Change the `cron` line in `forage.yml` for another schedule.

## How Keep and Skip work

Each card has Keep and Skip buttons. They open a new issue here, titled `keep: owner/name` or `skip: owner/name`. Submit it, and the feedback workflow records the mark in `feedback.yml`, replies, and closes the issue. Your marks (and your collaborators') count fully, and your Skip hides that repo for good. Other people's marks count a quarter as much, and they cannot hide anything. The `feedback:` section of `interests.yml` sets the limits, or turns visitor marks off.

## What is in this repo

| Path | What it is |
|---|---|
| `interests.yml` | What to look for. The only file you need to edit. |
| `feedback.yml` | Keep and Skip marks. The feedback workflow appends to it, and you can add marks by hand. |
| `state/` | What has been listed, star counts, and every run's digest. Written by the workflow. |
| `.github/workflows/forage.yml` | Weekly: forage, commit `state/`, build and deploy the portal. |
| `.github/workflows/feedback.yml` | On new issues: fold Keep and Skip into `feedback.yml`. |

## Security

- The workflows need no secrets. They use the repo's own `GITHUB_TOKEN`, with only the permissions each job needs.
- Every action, and gitforage itself, is pinned by a full commit SHA. Dependabot proposes updates to the actions as pull requests. Update `GITFORAGE_SHA` yourself when you want a newer gitforage.
- Issue text never reaches a shell. gitforage accepts only the exact `keep: owner/name` or `skip: owner/name` title, ignores bots and brand-new accounts, and rate-limits visitors.
- The portal is static HTML with a strict Content-Security-Policy and no third-party scripts, unless you turn on GoatCounter analytics.

More detail: [gitforage on GitHub](https://github.com/iacsha/gitforage).
