---
name: update-github-info
on:
  schedule: daily
  workflow_dispatch:

permissions:
  contents: read
  pull-requests: read

engine: copilot

tools:
  github:
    toolsets: [repos]
  edit:
  web-fetch:

network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com

safe-outputs:
  create-pull-request:
    title-prefix: "[github-info] "
    draft: true
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

Refresh `site/content/github-info.md` with concise, practical GitHub guidance for Mona's website.

## Sources and Constraints

1. Use GitHub repository API tools to read `notes/mona-notes.md` and the current `site/content/github-info.md`. Do not use terminal, CLI, or sandboxed commands for repository guidance or reference files.
2. Fetch and review https://github.blog/latest/ and https://github.blog/changelog/ with web-fetch.
3. Fetch and review the Awesome Copilot workflows page at https://awesome-copilot.github.com/workflows/ with web-fetch.
4. Select only useful, current updates that help developers learn GitHub faster. Keep the content concise and preserve the existing document structure unless a change is necessary.
5. Cite the GitHub Blog, GitHub Changelog, or Awesome Copilot workflows source for every external update you add.
6. Use the `create_pull_request` safe output to open a draft pull request for Mona to review. Include a short summary of the source-backed changes and do not modify any other file.