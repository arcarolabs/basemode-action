# Basemode design tokens

Sync Figma variables and styles to code with a pull request. No code changes needed.

```yaml
# .github/workflows/tokens.yml
name: Sync design tokens
on:
  schedule:
    - cron: "0 22 * * 0-4"
  workflow_dispatch:

permissions:
  contents: write
  pull-requests: write

jobs:
  tokens:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: arcarolabs/basemode-action@v1
        with:
          basemode-key: ${{ secrets.BASEMODE_KEY }}
          formats: tailwind4,typescript
          path: src/tokens
```

## Where tokens come from

| Input | Figma plan |
| --- | --- |
| `basemode-key`, from your design system's settings | Any, using the Basemode plugin |
| `figma-token` and `figma-file-keys` | Enterprise for variables; published styles on any plan |

## Inputs

| Input | Default | |
| --- | --- | --- |
| `path` | `src/tokens` | Folder the tokens go in |
| `formats` | `css` | Comma-separated: `css`, `scss`, `tailwind4`, `tailwind3`, `typescript`, `dtcg`, `storybook` |
| `color` | `hex` | `hex`, `rgb`, `hsl` or `oklch` |
| `unit` | `px` | `px`, `rem` or `em` |
| `prefix` | | Put in front of every token's name |
| `rename-references` | `true` | Update code that uses renamed tokens |
| `base` | Default branch | Branch to open the pull request against |
| `branch` | `basemode/tokens` | Branch the tokens are pushed to |
| `github-token` | `github.token` | Token that pushes the branch and opens the pull request |
| `basemode-api` | `https://api.basemode.dev` | Basemode's address |

The repository needs "Allow GitHub Actions to create and approve pull requests" turned on under Settings, Actions, General.

## Outputs

`pull-request`: the address of the pull request, when tokens changed.
