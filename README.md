# ATTENTION
This repository is no longer recommended. Feast your eyes upon https://github.com/reload/action-style-quality/ instead.

# action-stylelint
GitHub action examples that runs stylelint and reports the result to reviewdog.

# Prerequisites

Make use of [DAFT](https://github.com/reload/daft):

```sh
npm install @reloaddk/drupal --save-dev
```

or install the required dependencies directly:

```sh
npm install stylelint @reloaddk/stylelint-recommended --save-dev
```

# Usage

Under most circumstances we would also like a `.stylelintrc` file.

The minimum configuration should in most cases extend from [@reloaddk/stylelint-recommended](https://github.com/reload/stylelint#readme) and look like this:

```json
{
  "extends": ["@reloaddk/stylelint-recommended"]
}
```

Place it in your workdir, which depending on your configuration might be in a theme or at project root level.

## Root configuration

```yaml
on: pull_request
name: Stylelint
jobs:
  stylelint-reviewdog:
    name: reviewdog:SCSS
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2

    - name: Setup Node
      uses: actions/setup-node@v1
      with:
        node-version: '16'

    - name: Install dependencies
      uses: bahmutov/npm-install@HEAD

    - name: Run stylelint
      uses: reviewdog/action-stylelint@v1
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        stylelint_input: 'web/themes/custom/custom-theme/src/scss/**/*.scss'
```

## Theme configuration

```yaml
on: pull_request
name: Stylelint
jobs:
  stylelint-reviewdog:
    name: reviewdog:SCSS
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2

    - name: Setup Node
      uses: actions/setup-node@v1
      with:
        node-version: '16'

    - name: Install dependencies
      uses: bahmutov/npm-install@HEAD
      with:
        working-directory: web/themes/custom/custom-theme

    - name: Run stylelint
      uses: reviewdog/action-stylelint@v1
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        workdir: web/themes/custom/custom-theme
        stylelint_input: 'src/scss/**/*.scss'
```

