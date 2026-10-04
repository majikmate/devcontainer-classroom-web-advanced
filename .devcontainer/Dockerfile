# SPDX-License-Identifier: MIT
# © 2026 Hannes Stauss (scalarion@nimblescape.com)
# Licensed under the MIT License. See LICENSE in the repository root for details.

# devcontainer-classroom-web-advanced: the base image plus the native
# libraries of the Playwright browsers and the HTML validator.
#
# The layer tool devcon of devcontainer-core installs every layer.
# Layers and their arguments: https://github.com/majikmate/devcontainer-core/blob/main/docs/layers.md
FROM ghcr.io/majikmate/devcontainer-base:2

# playwright-deps: system libraries of the Playwright browsers (the projects
# install the browsers themselves)
ARG PLAYWRIGHT_BROWSERS="chromium firefox webkit"
RUN devcon install playwright-deps

# html-validate: VS Code extension HTML-validate (offline HTML5 validator) and
# the global configuration /.htmlvalidate.json, which fits Prettier
RUN devcon install html-validate
