# devcontainer-classroom-web-advanced: the base image plus the native
# libraries of the Playwright browsers.
#
# The layer tool devenv of devcontainer-core installs every layer.
# Layers and their arguments: https://github.com/majikmate/devcontainer-core/blob/main/docs/layers.md
FROM ghcr.io/majikmate/devcontainer-base:2

# playwright-deps: system libraries of the Playwright browsers (the projects
# install the browsers themselves)
ARG PLAYWRIGHT_BROWSERS="chromium firefox webkit"
RUN devenv install playwright-deps
