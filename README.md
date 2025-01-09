# Drop Staging Repository on Maven Central OSSRH

This GitHub Action drops a Sonatype staging repository on Maven Central using the [Nexus REST API](https://s01.oss.sonatype.org).

## Contents

- [Inputs](#inputs)
- [Example Usage](#example-usage)
- [How It Works](#how-it-works)
- [License](#license)

---

## Inputs

| Name                      | Description                                   | Required | Default |
|---------------------------|-----------------------------------------------|----------|---------|
| `repo-id`                | The staging repository ID to drop.            | **Yes**  |         |
| `maven-central-username` | Sonatype Username for Maven Central.          | **Yes**  |         |
| `maven-central-password` | Sonatype Password for Maven Central.          | **Yes**  |         |

---

## Example Usage

Below is an example of how you might call this action in a workflow.  
Save it in your repository as `.github/actions/drop-staging-repo/action.yml`, or wherever you keep custom actions:

```yaml
name: "Drop a Staging Repository"

on:
  workflow_dispatch:

jobs:
  drop-staging-repo:
    runs-on: ubuntu-latest
    steps:
      - name: Check out repository
        uses: actions/checkout@v3

      - name: Drop a staging repo
        uses: ./.github/actions/drop-staging-repo
        with:
          repo-id: "my.example.repo-1001"
          maven-central-username: ${{ secrets.MAVEN_CENTRAL_USERNAME }}
          maven-central-password: ${{ secrets.MAVEN_CENTRAL_PASSWORD }}
```
