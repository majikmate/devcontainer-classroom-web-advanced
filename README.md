# Devcontainer Classroom Web Advanced

A [Dev Container](https://containers.dev/) image for advanced web development
in the classroom, with AI assistance and modern testing tools.

Published image: `ghcr.io/majikmate/devcontainer-classroom-web-advanced`
(linux/amd64 and linux/arm64)

- Built on [`devcontainer-base`](https://github.com/majikmate/devcontainer-base)
  (`ghcr.io/majikmate/devcontainer-base:2`, Debian 13 "trixie"), which builds on
  [`devcontainer-core`](https://github.com/majikmate/devcontainer-core)
- Rebuilt and released automatically when the base image or one of the tools
  gets a new version
- GitHub Copilot is available (built into VS Code)

## Use it in an assignment repository

Add `.devcontainer/devcontainer.json` to the assignment (template) repository:

```jsonc
{
  "name": "Classroom Advanced",
  "image": "ghcr.io/majikmate/devcontainer-classroom-web-advanced:2",
}
```

- `:2` receives all compatible updates (new tool versions, security updates).
- `:1` is the old Debian 12 "bookworm" image and gets no more updates.

New Codespaces use the current image. With a local Docker installation, the
image stays cached. To get the newest version, run
`docker pull ghcr.io/majikmate/devcontainer-classroom-web-advanced:2` and then
**Dev Containers: Rebuild Container**.

## Included tools

From the base image:

- **Node.js** — newest LTS release, with npm (no pnpm)
- **Deno** — newest LTS release, the JavaScript/TypeScript runtime and language
  server in VS Code
- **Go** — newest release
- **Prettier** — the only formatter, standard style, Tailwind CSS class sorting
- **Git** — configured for simple workflows (auto fetch, rebase on sync)

Added by this image:

- **Playwright browser dependencies** — the native libraries for Chromium,
  Firefox and WebKit (layer `playwright-deps` of devcontainer-core, one line in
  [`.devcontainer/Dockerfile`](.devcontainer/Dockerfile)). Playwright itself is
  installed in each project (`npm install -D @playwright/test`).

The exact versions of each release are listed in its
[release notes](https://github.com/majikmate/devcontainer-classroom-web-advanced/releases).

### Formatting and code quality

- Files are formatted with Prettier when they are saved, with the **standard
  Prettier style** and 2-space indentation. **Tailwind CSS classes are sorted**
  into the standard order. A project with its own Prettier configuration uses
  that file instead.
- ESLint fixes all fixable problems on save (`source.fixAll.eslint`).

### VS Code extensions

In addition to the extensions of the base image (Go, Deno, Prettier, Markdown
preview, PlantUML):

- [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
- [GitHub Pull Requests](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github)
  — issues and pull requests (branch names and pull request defaults are
  pre-configured)
- [Live Preview](https://marketplace.visualstudio.com/items?itemName=ms-vscode.live-server)
  — opens in the external browser and serves the `dist` folder
- [Lorem Ipsum](https://marketplace.visualstudio.com/items?itemName=tyriar.lorem-ipsum)
- [Tailwind CSS IntelliSense](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss)
- [ES7+ React/Redux/React-Native Snippets](https://marketplace.visualstudio.com/items?itemName=dsznajder.es7-react-js-snippets)
- [Vitest](https://marketplace.visualstudio.com/items?itemName=vitest.explorer)
- [Playwright Test](https://marketplace.visualstudio.com/items?itemName=ms-playwright.playwright)

GitHub Copilot is built into VS Code and needs no extension. Students need
Copilot access, for example free through
[GitHub Education](https://education.github.com/).

### Classroom settings

- Extension recommendations are turned off.
- The folder `.devcontainer` is hidden.
- The user in the container is `dev`.

## Automatic releases

The workflow [`.github/workflows/release.yml`](.github/workflows/release.yml)
uses the shared workflow of `devcontainer-core` (described in its
[README](https://github.com/majikmate/devcontainer-core#releases)):

- Every night at 03:57 UTC it checks whether the inputs of the image changed:
  the `.devcontainer` folder and the digest of the base image. The base image
  runs its check two hours earlier and is rebuilt when a tool gets a new
  version, so new tool versions reach this image in the same night.
- To get a new image at once, open **Actions → Release → Run workflow** and
  keep the default options. With the option `upstream` (on by default), the run
  first starts the Release workflow of devcontainer-base and waits for it;
  devcontainer-base first starts devcontainer-core in the same way. Each image
  in the chain gets a new release only if one of its inputs changed, for
  example a new Go, Node.js or Deno version. Then the run checks this image and
  releases a new version if an input changed. The option `force` releases a new
  version of this image without a change. See
  [Schedule and chain build](https://github.com/majikmate/devcontainer-core#schedule-and-chain-build)
  for the GitHub App.
- A push to `main` with changes in `.devcontainer` releases a new version.
- Pull requests are built and tested (both architectures) without publishing.
- A tag `vX.Y.Z` releases exactly this version.

Each release is built without cache, tested inside the container (the tests of
all layers: user, SSH server, Go, Node.js, Deno, Prettier with Tailwind CSS
sorting, Playwright libraries),
and gets the tags `X.Y.Z`, `X.Y`, `X` and `latest` and a GitHub release with the
installed versions.

## Customization

Edit `.devcontainer/devcontainer.json` through a pull request. After the merge,
the new image is released automatically.
