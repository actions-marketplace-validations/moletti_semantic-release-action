# Github Action: Semantic Release
GitHub Action for Semantic Release

# Requirements
.releaserc - Semantic Release configuration file, for more info see [semantic-release documentation](https://github.com/semantic-release/semantic-release/blob/master/docs/usage/configuration.md#configuration-file)
```yaml
# example .relesearc
{
    "branches": ["master"],
    "plugins": [
        "@semantic-release/commit-analyzer",
        "@semantic-release/release-notes-generator",
        "@semantic-release/github",
        [
            "@semantic-release/changelog",
            {
                "changelogFile": "CHANGELOG.md",
                "changelogTitle": "# Changelog"
            }
        ],
        [
            "@semantic-release/git",
            {
                "assets": [
                    "CHANGELOG.md"
                ]
            }
        ],

    ]
}
```

# Example Usage
```yaml
name: Release
on:
  push:
    branches:
      - master

jobs:
  release:
    name: Release
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v2
        with:
          fetch-depth: 0
      - name: Release
        uses: moletti/semantic-release-action@v1
        env:
          GITHUB_TOKEN: ${{ secrets.GH_TOKEN }}
```