# Changelog render GitHub action

Renders a changelog for a release or something like that.

# Usage


## Inputs

##### `long_changelog_export_filename`

Path for long changelog to export into

Default: `.changelog_long.md`

##### `short_changelog_export_filename`

Path for short changelog to export into 

Default: `.changelog_short.md`

##### `long_changelog_format`

Format for long changelog

Documentation: https://git-scm.com/docs/pretty-formats

Default: `%w(1000)* %cd %an <%ae>%n%w(1000,0,2)- %s%n`

##### `short_changelog_format`

Format for short changelog

Documentation: https://git-scm.com/docs/pretty-formats

Default: `%w(200,0,2)- %s (%an <%ae>)`

##### `changelog_ref_start`

Ref to start changelog from 

Default: last tag

##### `changelog_ref_end`

Ref to start changelog from 

Default: HEAD

##### `changelog_header`

Header before the actual changelog

Default: `# Changelog`

##### `print_out_changelogs`

Whether to print out rendered changelogs or not

Default: false


## Outputs

* `long_changelog_filename` - Rendered long changelog filename
* `short_changelog_filename` - Rendered short changelog filename

# Usage

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

      - name: Generate changelog
        id: changelog_render
        uses: reinvented-stuff/changelog-render-action@master
        with:
          long_changelog_export_filename: ".long_changelog.md"
          short_changelog_export_filename: ".short_changelog.md"
          print_out_changelogs: true
...

```

# Changelog examples

### Default long changelog format

```
* Sun Jun 12 2022 Pavel Kim <hello@pavelkim.com>
- [Fix] Double changelog output after a copy-paste

* Sun Jun 12 2022 Pavel Kim <hello@pavelkim.com>
- [Fix] Mixed up bash and github variable reference formats

* Sun Jun 12 2022 Pavel Kim <hello@pavelkim.com>
- [Fix] Input not defined at all and raises an error when referenced if not passed when calling

* Sun Jun 12 2022 Pavel Kim <hello@pavelkim.com>
- [Change] Version bump

* Sun Jun 12 2022 Pavel Kim <hello@pavelkim.com>
- [Change] Even more improved readability in readme

* Sun Jun 12 2022 Pavel Kim <hello@pavelkim.com>
- [Change] Improved readability, added all input defaults in readme

* Sun Jun 12 2022 Pavel Kim <hello@pavelkim.com>
- [Change] Github Workflow now uses changelog-render-action instead of manual implementation

* Sun Jun 12 2022 Pavel Kim <hello@pavelkim.com>
- [Add] Initial state
```

### Default short changelog format

```
- [Fix] Double changelog output after a copy-paste (Pavel Kim <hello@pavelkim.com>)
- [Fix] Mixed up bash and github variable reference formats (Pavel Kim <hello@pavelkim.com>)
- [Fix] Input not defined at all and raises an error when referenced if not passed when calling (Pavel Kim <hello@pavelkim.com>)
- [Change] Version bump (Pavel Kim <hello@pavelkim.com>)
- [Change] Even more improved readability in readme (Pavel Kim <hello@pavelkim.com>)
- [Change] Improved readability, added all input defaults in readme (Pavel Kim <hello@pavelkim.com>)
- [Change] Github Workflow now uses changelog-render-action instead of manual implementation (Pavel Kim <hello@pavelkim.com>)
- [Add] Initial state (Pavel Kim <hello@pavelkim.com>)
```
