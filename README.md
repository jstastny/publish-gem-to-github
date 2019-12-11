# Release Ruby Gem to GitHub Packages
This action builds the gems for all `.gemspec` files in the projects root and uploads them to [GitHub Packages](https://github.com/features/packages).

## Usage
Example minimal workflow using this action:
```yaml
name: CI

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v1
    - name: Build and publish gem
      uses: jstastny/publish-gem-to-github@master
      with:
        token: ${{ secrets.GITHUB_TOKEN }}
        owner: jstastny
```

See example project using this action at [https://github.com/jstastny/testgem](https://github.com/jstastny/testgem).

## Inputs

| Name | Description |
| -----| ------------|
| `token` | GitHub token that has write access to Packages. You can use `secrets.GITHUB_TOKEN` |
| `owner` | Name of the user or organization account that owns the repository containing your project |

## Versioning your gem

This action currently does not bump the gem's version when building it. It is up to you to do it (either manually or in a previous workflow step).
If you try to release gem in the same version that already exists, the step will fail.
