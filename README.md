# shared-security-workflows

The idea with this repository is to simulate a central repository of workflows that are shared across an entire Github org. An organization might create a number of security workflows that are shared across all repositories in this way.  

## Trivy License Scanning

The Trivy license scan workflow is implemented in `.github/workflows/trivy-license.yaml`, with an accompanying config file, `workflows/trivy-config.yaml.` Licenses added to the forbidden section of the config file will cause the workflow to exit non-zero if any of the licenses are present in the target repo being scanned.

The idea is to implement the license scanning as a shared workflow that is called across all repos in the org when a pull request is created in each repo. If a forbidden license is being introduced by the change in the pull request, then the license scan will fail, hence blocking the pull request.

The current implementation uses a static target repo, grafana/grafana, and is triggered by a `workflow_dispatch` trigger.
