# Changelog render GitHub action

renders a changelog

# Usage


## Inputs

* `long_changelog_export_filename` - Path for long changelog to export into (default: `.changelog_long.md`)
* `short_changelog_export_filename` - Path for short changelog to export into (default: `.changelog_short.md`)
* `long_changelog_format` - Format for long changelog
* `short_changelog_format` - Format for short changelog
* `changelog_ref_start` - Ref to start changelog from (default: last tag)
* `changelog_ref_end` - Ref to start changelog from (default: HEAD)
* `print_out_changelogs` - Whether to print out rendered changelogs or not

## Outputs

* `long_changelog_filename` - Rendered long changelog filename
* `short_changelog_filename` - Rendered short changelog filename

# Example

```yaml
---
name: Release

on:
  push:
    branches:
      - "*"

jobs:
  changelog_render:
    name: Render a changelog
    runs-on: ubuntu-latest
    outputs:
      long_changelog_filename: ${{ steps.changelog_render.outputs.long_changelog_filename }}
      short_changelog_filename: ${{ steps.changelog_render.outputs.short_changelog_filename }}

    steps:

      - name: Check out code
        uses: actions/checkout@v2
        with:
          fetch-depth: 0

      - name: Use latest released action
        id: changelog_render
        uses: reinvented-stuff/changelog-render-action@master
        with:
          long_changelog_export_filename: ".long_changelog.md"
          short_changelog_export_filename: ".short_changelog.md"
          print_out_changelogs: true
...

```