# ModMaster Release Action

This GitHub Action is solely for using the [ModMaster Gradle Plugin](https://github.com/ToCraft/ModMaster).

Here's a working example:

```yml
name: Release

on:
  push:
    paths:
      - '**.gradle'
      - '**.gradle.kts'
      - '**.properties'
      - '**/src/**'
    branches:
      - "main"
      - "master"
      - "1.**"
  workflow_dispatch:

permissions:
  contents: write
  actions: write

jobs:
  build:
    runs-on: ubuntu-latest
    if: |
      !contains(github.event.head_commit.message, '[ci skip]')
    steps:
      - uses: ToCraft/modmaster-release-action@v2
        with:
          java-version: '25'
          maven-pass: ${{ secrets.MAVEN_PASS }}
          curseforge-token: ${{ secrets.CURSEFORGE_TOKEN }}
          modrinth-token: ${{ secrets.MODRINTH_TOKEN }}
          webhook: ${{ secrets.DISCORD_WEB_HOOK }}
```

---

Using the script at `.github/workflows/update-tags.yml` you can auto-update the tags by running:
```bash
git tag v2.0.1
git push origin v2.0.1
```
