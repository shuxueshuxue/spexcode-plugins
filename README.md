# spexcode-plugins

SpexCode's agent add-ons, as one marketplace root.

This repository is **mirrored** from [`spexcode`](https://github.com/shuxueshuxue/spexcode)'s
`distribution/` directory by CI. Nothing here is edited by hand — open changes against that directory.

It exists so installing a skill does not mean cloning the product repository: both hosts clone the whole
repository a marketplace names, and the `owner/repo` form reads the manifest only at the repository root.

## Install

**Claude Code**

    claude plugin marketplace add shuxueshuxue/spexcode-plugins
    claude plugin install atlas@spexcode

**Codex**

    codex plugin marketplace add shuxueshuxue/spexcode-plugins
    codex plugin add atlas@spexcode

`penguin/`, `zcode/` and `gugu/` are installed through their own hosts' mechanisms.
