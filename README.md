# We the collective

We’re a fast-moving independent creative agency helping gaming, toys, sports, and entertainment brands build generational fandom.

## Org lint check

[`.github/workflows/lint.yml`](.github/workflows/lint.yml) runs as the **Org lint / lint** check on every pull request (and merge queue group) in every repo in the org. It's required by an organization ruleset, which is managed separately in Terraform. You don't need to copy the workflow into your repo, and you can't turn it off there.

What it runs depends on the repo:

1. **`package.json` has a `lint` script.** It sets up Node from `.nvmrc`, or from `engines.node` in `package.json`, and falls back to the current LTS. It installs dependencies with the package manager matching your lockfile (`package-lock.json` → npm, `pnpm-lock.yaml` → pnpm, `yarn.lock` → yarn), with caching, then runs `lint`.
2. **No lint script, but there are workflow files.** It runs [actionlint](https://github.com/rhysd/actionlint) on `.github/workflows`.
3. **Neither.** It passes and adds a "No lint script found, skipped" notice to the job summary.

To opt in, add a `lint` script to `package.json`, for example `"lint": "eslint ."`, and commit your lockfile. The check has a 10-minute timeout, and a new push to a PR cancels the run already in progress.
