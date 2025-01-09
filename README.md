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

```yaml
name: "Drop a Staging Repository"

on:
  workflow_dispatch:

jobs:
  staging-repo:
    runs-on: ubuntu-24.04
    outputs:
      staging-repo-id: ${{ steps.create-staging-repo.outputs.staging-repo-id }}
    steps:
      - id: create-staging-repo
        name: Create a staging repository
        uses: danysk/action-create-ossrh-staging-repo@1.0.0
        with:
          group-id: "org.danilopianini"
          maven-central-username: ${{ secrets.MAVEN_CENTRAL_USERNAME }}
          maven-central-password: ${{ secrets.MAVEN_CENTRAL_PASSWORD }}
  drop-staging-repo:
    needs: staging-repo
    runs-on: ubuntu-24.04
    steps:
      - name: Drop a staging repository
        uses: danysk/action-drop-ossrh-staging-repo@1.0.0
        with:
          repo-id: ${{ needs.staging-repo.outputs.staging-repo-id }}
          maven-central-username: ${{ secrets.MAVEN_CENTRAL_USERNAME }}
          maven-central-password: ${{ secrets.MAVEN_CENTRAL_PASSWORD }}
```
