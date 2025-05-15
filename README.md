# Multi-Checker Pipeline
This workflow is a reusable workflow to run a series of preflight checks on your code. The checks include:

* **[Repolinter](https://github.com/qualcomm-linux/qli-actions)**: Checks the repository for consistency and adherence to coding standards.
* **[Semgrep](https://github.com/qualcomm-linux/qli-actions)**: Runs a static analysis tool to detect potential security vulnerabilities and coding errors.
* **[Copyright-License-Detector](https://github.com/qualcomm/copyright-license-checker-action)**: Checks for proper copyright and licensing information in the code.
* **[PR-Check-Emails](https://github.com/qualcomm/commit-emails-check-action)**: Verifies that the commit emails are properly formatted.

## Example
You can use this workflow in your repository by adding the following code to your `.github/workflows` directory:

```
name: preflight-checkers 
on:
  pull_request:
    branches: ["main", "master"]
  push:
    branches: ["main", "master"]
  workflow_dispatch:

jobs:
  checker:
    uses: qualcomm-linux/multi-checker-pipeline/.github/workflows/checker.yml@main
    with:
        repolinter: true # default: false
        semgrep: true # default: false
        copyright-license-detector: true # default: false
        pr-check-emails: true # default: false

    secrets:
      SEMGREP_APP_TOKEN: ${{ secrets.SEMGREP_APP_TOKEN }}
```
