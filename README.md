# commitlint

A GitHub action to run commitlint CLI Checks.

## Usage

```yml
jobs:
  commitlint:
    runs-on: ubuntu-latest
    steps:
      # For getting the commitlint config
      - name: Checkout Repository
        uses: actions/checkout@v4
        with:
           fetch-depth: 0

      - name: Run commitlint
        uses: dafnik/commitlint@v1
        with:
          #commitlint_version: 'latest'
```

<!-- prettier-ignore-start -->
| Inputs               | Required | Description                  |
|----------------------|----------|------------------------------|
| `commitlint_version` |          | Version of commitlint to use |
<!-- prettier-ignore-end -->

Furthermore, see [action.yml](action.yml)

## Release instructions

In order to release a new version of this action:

1. Locate the semantic version of the [upcoming release][release-list] (a draft is maintained by the [`draft-release` workflow][draft-release]).

2. Publish the draft release from the `main` branch with semantic version as the tag name, _with_ the checkbox to publish to the GitHub Marketplace checked. :ballot_box_with_check:

3. After publishing the release, the [`release` workflow][release] will automatically run to create/update the corresponding the major version tag such as `v0`.

   ⚠️ Environment approval is required. Check the [Release workflow run list][release-workflow-runs].

## License

The scripts and documentation in this project are released under the [MIT License](LICENSE).

<!-- references -->

[release-list]: https://github.com/dafnik/commitlint/releases
[draft-release]: .github/workflows/draft-release.yml
[release]: .github/workflows/release.yml
[release-workflow-runs]: https://github.com/dafnik/commitlint/actions/workflows/release.yml