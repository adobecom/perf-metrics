perf-metrics
Playwright-based performance check for GitHub repos. Measures LCP, CLS, TBT, JS size/total size, compares PR vs base, and comments results on PRs. Non-blocking by default.

## PR comment workflow (reusable)

The workflow `.github/workflows/pr-comment-from-perf-metrics.yaml` can be used from **other repositories**. When a PR is opened in that repo, it runs and posts a comment: *"It is running from perf-metrics repo"*.

### Using it in another repo

1. In the other repo, create a workflow (e.g. `.github/workflows/use-perf-metrics-comment.yml`) that triggers on PR open and calls this reusable workflow:

```yaml
name: Use perf-metrics PR comment

on:
  pull_request:
    types: [opened]

jobs:
  pr-comment:
    uses: OWNER/perf-metrics/.github/workflows/pr-comment-from-perf-metrics.yaml@main
```

2. Replace `OWNER` with the GitHub org or user that owns the `perf-metrics` repo (e.g. `adobecom` or your username).

3. Ensure the default `GITHUB_TOKEN` in the other repo has permission to write to pull requests (it does by default). No secrets are required.
