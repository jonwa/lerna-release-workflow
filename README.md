# Lerna Release Workflow

A basic [Lerna](https://lerna.js.org/) monorepo with [Yarn Workspaces](https://classic.yarnpkg.com/en/docs/workspaces/), [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) and [GitHub Actions workflow](https://github.com/features/actions) configuration to achieve fully automated package publishing to the GitHub Package Registry.

## Create a new repository from this template

Click the `Use this Template` button and provide the new repository details.

## Getting Started

Let's start by setting up the new repository:

1. Update the root `package.json` with your repository name and url.

2. Rename `packages/package-a` and `packages/package-b` to suit your needs and don't forget to update their `package.json`.

   > **NOTE:** For a package to be releasable to GitHub Package Registry, it must be scoped to match the owner of the repository. The package name is optional, as long as it is unique under that scope. In addition, the `repository.url` field needs to be consistent in all package.json files.

3. Run `yarn bootstrap` to bootstrap the packages. This will install all of their dependencies and links any cross-dependencies.

## How it works

Each push to `master` branch will generate a version number, git tag, Conventional Changelog, release commit, pushing changes to the origin and publish your packages to GitHub Package Registry.

# License

The scripts and documentation in this project are released under the [MIT License](LICENSE)
