# Release Ruby Gem to GitHub Packages
This action builds the gems for all `.gemspec` files in the projects root and uploads them to [GitHub Packages](https://github.com/features/packages) (or optionally specify a subdirectory to build from).

## Usage
Example minimal workflow using this action:
```yaml
name: CI

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest
    permissions:
      packages: write
      contents: read

    steps:
    - uses: actions/checkout@v2
    - name: Build and publish gem
      uses: jstastny/publish-gem-to-github@master
      with:
        token: ${{ secrets.GITHUB_TOKEN }}
        owner: jstastny
```

See example project using this action at [https://github.com/jstastny/testgem](https://github.com/jstastny/testgem).

## Inputs

| Name                | Description                                                                                     |
| ------------------- | ----------------------------------------------------------------------------------------------- |
| `token`             | GitHub token that has write access to Packages. You can use `secrets.GITHUB_TOKEN`              |
| `owner`             | Name of the user or organization account that owns the repository containing your project       |
| `working-directory` | Optional parameter of the directory where you wish to build your gemspecs in (defaults to root) |
| `permissions`       | Default value for packages in permissions is read only, You need to set it to write             |

## Versioning your gem

This action currently does not bump the gem's version when building it. It is up to you to do it (either manually or in a previous workflow step).
If you try to release gem in the same version that already exists, the step will fail.

In case you want to ignore these types of failures, you can add:
```
continue-on-error: true
```
to the build step configuration.
