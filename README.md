# Devcontainer Classroom Web Advanced

A [Dev Container](https://containers.dev/) configuration for advanced web
development classroom environments. This setup provides a consistent,
pre-configured development environment with AI assistance and modern testing
tools for educational use.

Published image: `ghcr.io/majikmate/devcontainer-classroom-web-advanced`

**Features:**

- Built on top of
  [`devcontainer-base`](https://github.com/majikmate/devcontainer-base)
- Multi-arch support (linux/amd64 and linux/arm64)
- Optimized for advanced web development education
- Includes AI-assisted development tools
- Pre-configured testing frameworks
- Pre-configured VS Code settings for classroom use

## Included Tools & Languages

All runtimes and core tooling come from the base image
(`ghcr.io/majikmate/devcontainer-base`):

### Languages & Runtimes

- **Go** - Latest version with proper formatting and linting
- **Node.js** - LTS version with pnpm and nvm for package management
- **Deno** - Modern TypeScript/JavaScript runtime

### Development Tools

- **Git** - Configured with classroom-optimized settings for smooth workflows
- **VS Code Extensions**:
  - [GitHub Copilot](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot)
    — AI-powered code completions
  - [GitHub Copilot Chat](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat)
    — AI-powered chat assistance
  - [Live Server](https://marketplace.visualstudio.com/items?itemName=ms-vscode.live-server)
    — real-time browser preview, opens in external browser
  - [Lorem Ipsum](https://marketplace.visualstudio.com/items?itemName=tyriar.lorem-ipsum)
    — placeholder text generator
  - [Tailwind CSS IntelliSense](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss)
    — autocomplete for Tailwind classes
  - [ES7+ React/Redux/React-Native Snippets](https://marketplace.visualstudio.com/items?itemName=dsznajder.es7-react-js-snippets)
    — shorthand snippets for React, Redux, and related patterns
  - [Vitest](https://marketplace.visualstudio.com/items?itemName=vitest.explorer)
    — testing framework integration
  - [Playwright](https://marketplace.visualstudio.com/items?itemName=ms-playwright.playwright)
    — end-to-end testing tools

### Classroom-Optimized Configuration

- GitHub Copilot enabled for AI-assisted learning and development
- Extension recommendations suppressed
- Configuration folders (`.devcontainer`, `.github`, `.vscode`) hidden from
  students to reduce clutter

## Getting Started

### Prerequisites

- [Docker](https://www.docker.com/get-started) installed on your system
- [VS Code](https://code.visualstudio.com/) with the
  [Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

### Using This Dev Container

1. **Clone or use as template**: Clone this repository or use it as a GitHub
   template for your classroom project

2. **Open in VS Code**: Open the project folder in VS Code

3. **Reopen in Container**: When prompted, click "Reopen in Container" or use
   the command palette (`Ctrl+Shift+P` / `Cmd+Shift+P`) and select "Dev
   Containers: Reopen in Container"

4. **Wait for setup**: The container will pull and start automatically (first
   time may take a few minutes)

### For Instructors

This configuration is designed to provide students with a consistent, advanced
development environment. Key benefits:

- No need for students to install development tools locally
- Consistent environment across different operating systems (amd64 & arm64)
- AI-assisted development with GitHub Copilot (requires student licenses)
- Modern testing tools (Vitest, Playwright) pre-installed
- Hidden config folders keep the workspace clutter-free for students

**Note:** Students will need GitHub Copilot access (available free through
[GitHub Education](https://education.github.com/)) to use AI features.

### Customization

Modify the development container by editing `.devcontainer/devcontainer.json`:

- Add or remove VS Code extensions in the `extensions` array
- Adjust VS Code settings under `customizations.vscode.settings`

## CI/CD

A GitHub Actions workflow (`.github/workflows/publish-devcontainer.yml`)
automatically builds and publishes the container image to the GitHub Container
Registry:

- **On push to `main`**: Builds both architectures and updates the build cache
- **On version tag (`v*`)**: Builds, pushes per-arch images, and creates a
  multi-arch manifest with `latest` and semver tags
- **On pull request** (touching `.devcontainer/**` or `.github/**`): Build-only
  validation without pushing

## Contributing

When contributing to this classroom environment:

1. Test changes thoroughly in a development container
2. Update documentation as needed
3. Consider the impact on student experience
4. Ensure consistency across different platforms
