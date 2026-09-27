# devcontainer-classroom-web-advanced

The classroom image for advanced web development, with AI assistance, ESLint,
Vitest and Playwright.

**Image:** `ghcr.io/majikmate/devcontainer-classroom-web-advanced:2` ·
linux/amd64, linux/arm64 ·
[release notes](https://github.com/majikmate/devcontainer-classroom-web-advanced/releases)

## Dependencies

```text
                                               Nightly Content
devcontainer-features                                  Go library of layers, compiled into devcon
  ▼
devcontainer-core:1                            23:17   Debian 13, devcon, user dev, zsh, SSH server
├── devcontainer-base:2                        01:17   + go, build-tools, node, deno, prettier
│   ├── devcontainer-dev:2                     03:37   + github-cli
│   ├── devcontainer-classroom-web:2           03:47   classroom settings, AI off
│   └── devcontainer-classroom-web-advanced:2  03:57   + playwright-deps, AI on
└── devcontainer-classroom-exam-ts:2           01:27   + deno, AI and coding assistance off
```

This repository: **devcontainer-classroom-web-advanced**. Nightly checks in
UTC. Repositories: [core](https://github.com/majikmate/devcontainer-core) ·
[features](https://github.com/majikmate/devcontainer-features) ·
[base](https://github.com/majikmate/devcontainer-base) ·
[dev](https://github.com/majikmate/devcontainer-dev) ·
[classroom-web](https://github.com/majikmate/devcontainer-classroom-web) ·
[classroom-web-advanced](https://github.com/majikmate/devcontainer-classroom-web-advanced) ·
[classroom-exam-ts](https://github.com/majikmate/devcontainer-classroom-exam-ts)

## Use

Add `.devcontainer/devcontainer.json` to the assignment (template) repository:

```jsonc
{
  "name": "Classroom Advanced",
  "image": "ghcr.io/majikmate/devcontainer-classroom-web-advanced:2",
}
```

- `:2` receives all compatible updates (new tool versions, security updates).
- A full version (for example `:2.0.5`) stays available for at least 90 days.
- With a local Docker installation, run
  `docker pull ghcr.io/majikmate/devcontainer-classroom-web-advanced:2` and
  then **Dev Containers: Rebuild Container** to get the newest version.

## Content

| Layer | Content | Version |
| ----- | ------- | ------- |
| (devcontainer-base) | Debian 13, user `dev`, zsh, SSH server; Go, Node.js with npm, Deno, Prettier with Tailwind CSS class sorting | see [base](https://github.com/majikmate/devcontainer-base#content) |
| `playwright-deps` | native libraries of the Playwright browsers Chromium, Firefox and WebKit | Debian packages |

Playwright itself is installed in each project
(`npm install -D @playwright/test`).

## VS Code

- **Extensions:** the extensions of the base image, plus
  [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint),
  [GitHub Pull Requests](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github),
  [Live Preview](https://marketplace.visualstudio.com/items?itemName=ms-vscode.live-server),
  [Lorem Ipsum](https://marketplace.visualstudio.com/items?itemName=tyriar.lorem-ipsum),
  [Tailwind CSS IntelliSense](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss),
  [ES7+ React Snippets](https://marketplace.visualstudio.com/items?itemName=dsznajder.es7-react-js-snippets),
  [Vitest](https://marketplace.visualstudio.com/items?itemName=vitest.explorer),
  [Playwright Test](https://marketplace.visualstudio.com/items?itemName=ms-playwright.playwright).
- **Formatting and code quality:** Prettier formats on save with the standard
  Prettier style and sorts Tailwind CSS classes; ESLint fixes all fixable
  problems on save.
- **AI:** GitHub Copilot is built into VS Code and turned on. Students need
  Copilot access, for example free through
  [GitHub Education](https://education.github.com/).
- **GitHub Pull Requests:** branch names and pull request defaults are set.
  Live Preview opens in the external browser and serves the folder `dist`.
- Extension recommendations are off. The folder `.devcontainer` is hidden.

## Releases

- **Nightly check at 03:57 UTC.** A new version is released when an input
  changes: `.devcontainer`, `README.md` or the digest of `devcontainer-base:2`. Pending
  Debian updates and an age above 7 days also lead to a new version.
- **Manual:** **Actions → Release → Run workflow**. The option `upstream` (on
  by default) first updates base and core; `force` releases without a change.
- **Pull requests** build and test both architectures and publish nothing.
- **Kept versions:** the newest release and the tags `2`, `2.x` and `latest`.
  Older releases and workflow runs are deleted after 90 days. **Actions →
  Prune** lists or deletes them at once; the scope `all-but-newest` keeps
  only the newest release and the newest run of each workflow.

Rules: [Releases](https://github.com/majikmate/devcontainer-core#releases).

## Change the image

Change `.devcontainer/` or `README.md` through a pull request and consider the
effect on the students. After the merge, the new image is released
automatically (GitHub shows the README of the newest image on the package
page).

## License

MIT
