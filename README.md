# emumba-skills-react

React and Next.js skills for Emumba, distributed to developers through the
LiteLLM gateway catalogue as the plugin `emumba-react`.

> **Status: draft.** Nothing in this repo is ratified Emumba policy yet.

## What is in here

| Skill | Scope |
|---|---|
| `react-best-practices` | React and Next.js performance — request waterfalls, bundle size, re-render cost, server/client boundaries |

## Layout is not negotiable

Claude Code discovers skills only at `<plugin-root>/skills/<name>/SKILL.md`, and
the plugin needs a `.claude-plugin/plugin.json`. A repo that nests skills by
category installs cleanly and loads **zero** skills, with no error anywhere.

This repo is therefore **plugin-at-root**: `.claude-plugin/` and `skills/` sit at
the top level, matching `emumba-skills-backend`. Register it with the `url`
git-source form — the `github` form makes Claude Code clone over SSH, which
fails on any machine without a github.com host key.

## Versioning

The version Claude Code honours is the one in `.claude-plugin/plugin.json` in
this repo — **not** the version shown in the LiteLLM dashboard. Bumping the
catalogue entry alone does not ship an update, and reports no error while doing
nothing. Shipping a change means bumping the manifest here and pushing.

Developers then need **both** commands; refreshing the catalogue alone does not
upgrade an installed plugin:

```bash
claude plugin marketplace update litellm
claude plugin update emumba-react@litellm
```

The source schema has no branch or ref field, so this plugin must live on the
default branch.

## Two delivery paths

The same `SKILL.md` reaches a developer two ways:

1. **Marketplace** — Claude Code clones this repo directly from GitHub. The
   gateway serves only metadata, never file content.
2. **Gateway injection** — the control-plane gateway appends the skill body to
   matching requests server-side, so the standard applies even on models that
   would never call the `Skill` tool.

Path 2 currently reads its own copy under `plugins/emumba-react/` in the
`control-plane-gateway` repo, so **the two paths are kept in step by hand.**
Nothing enforces that they agree, and drift would be silent. Reconciling this is
an open item.

## Attribution

`skills/react-best-practices` is **mirrored from a third-party MIT-licensed
repository** and is not original Emumba work. See [`ATTRIBUTION.md`](ATTRIBUTION.md)
before including it in any client deliverable — that file records the upstream
source, the declared licence and author, and what was changed.
