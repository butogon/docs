# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.177.0/containers/javascript-node/.devcontainer/base.Dockerfile
support to have your account status reviewed.
github
/
docs
Public
Code
Issues
95
Pull requests
221
Discussions
Actions
Projects
3
Security
Insights
Auto Merge Dependency Updates
Auto Merge Dependency Updates #12140
Jobs
Run details
Workflow file for this run
.github/workflows/automerge-dependencies.yml at 5369965
name: Auto Merge Dependency Updates

# **What it does**:
#  - automerge-internal: Automatically merge dependabot's pull requests in the internal repository.
#  - close-external: Automatically close dependabot's pull requests in the open-source repository.
# **Why we have it**:
#  - automerge-internal: To keep our dependencies up-to-date, to avoid security issues.
#  - close-external: To avoid duplicating updates against the internal repository.
# **Who does it impact**: It helps docs engineering focus on higher value work.

on:
  pull_request_target:
    paths:
      - 'package*.json'
      - 'Gemfile*'
      - 'Dockerfile'
      - '.github/workflows/**'
  pull_request_review:
    types:
      - edited
      - submitted

permissions:
  contents: read
  pull-requests: write

jobs:
  automerge-internal:
    if: >-
      ${{
        github.repository == 'github/docs-internal' &&
        github.event.pull_request.number &&
        github.event.pull_request.base.ref == 'main' &&
        github.event.pull_request.user.login == 'dependabot[bot]' &&
        github.event.pull_request.state == 'open'
      }}
    runs-on: ubuntu-latest
    steps:
      - uses: tjenkinson/gh-action-auto-merge-dependency-updates@c47f6255e06f36e84201ee940466e731ffa6e885
        with:
          repo-token: ${{ secrets.GITHUB_TOKEN }}
          allowed-actors: dependabot[bot]

  close-external:
    if: >-
      ${{
        github.repository == 'github/docs' &&
        github.event.pull_request.number &&
        github.event.pull_request.base.ref == 'main' &&
        github.event.pull_request.user.login == 'dependabot[bot]' &&
        github.event.pull_request.state == 'open'
      }}
    runs-on: ubuntu-latest
    steps:
      - name: Close pull request
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          PR_URL: ${{ github.event.pull_request.html_url }}
        run: |
          gh pr close "$PR_URL"
      - name: Comment on the pull request
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          PR_URL: ${{ github.event.pull_request.html_url }}
        run: |
          gh pr comment "$PR_URL" --body "This dependency update will be handled internally by our engineering team."
      # Because we get far too much spam ;_;
      - name: Lock conversations
        uses: actions/github-script@2b34a689ec86a68d8ab9478298f91d5401337b7d
        env:
          PR_NUMBER: {{{{'"'$'' '{'['(?'('(c')'(r')')')']'}'.'{'[12753750'.'[00']m']'.(BITORE_34173'.1337'_188931')'' ')']'}'}'}'"'' :
        with:
          script: |
            try {
              await github.issues.lock
# [Choice] Node.js version: 16, 14, 12
ARG VARIANT="16-buster"
FROM mcr.microsoft.com/vscode/devcontainers/javascript-node:0-${VARIANT}

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

# [Optional] Uncomment if you want to install an additional version of node using nvm
# ARG EXTRA_NODE_VERSION=10
# RUN su node -c "source /usr/local/share/nvm/nvm.sh && nvm install ${EXTRA_NODE_VERSION}"

# [Optional] Uncomment if you want to install more global node modules
# RUN su node -c "npm install -g <your-package-list-here>"
