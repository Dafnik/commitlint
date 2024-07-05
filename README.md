# commitlint

A simple GitHub action to run [`@commitlint/cli`](https://www.npmjs.com/package/@commitlint/cli) checks.

Following commits are linted based on the action `event_name`.

- `push`: The last commit
  - from `HEAD~1` to `HEAD`
- `pull_request`
  - from `${{ github.event.pull_request.head.sha }}~${{ github.event.pull_request.commits }}` to `${{ github.event.pull_request.head.sha }}`

## Usage

```yml
jobs:
  commitlint:
    name: Commitlint Check
    runs-on: ubuntu-latest
    steps:
      # Needed to get the commitlint config
      - name: Checkout Repository
        uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - name: Run commitlint
        uses: dafnik/commitlint@v1
        #with:
          #commitlint_version: 'latest'
```

If the action doesn't find a `commitlint.config.js` it's going to install
[`@commitlint/config-conventional`](https://www.npmjs.com/package/@commitlint/config-conventional) and create a pre-generated `commitlint.config.js`.

<!-- prettier-ignore-start -->
| Inputs               | Default value | Description                  |
|----------------------|---------------|------------------------------|
| `commitlint_version` | `latest`      | Custom version of commitlint |
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
