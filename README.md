# Lerna Release Workflow

A basic [Lerna](https://lerna.js.org/) monorepo with [Yarn Workspaces](https://classic.yarnpkg.com/en/docs/workspaces/), [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) and [GitHub Actions workflow](https://github.com/features/actions) configuration to achieve fully automated package publishing to the GitHub Package Registry.

## Create a new repository from this template

Click the `Use this template` button and provide the new repository details.

## Getting Started

Let's start by setting up the new repository:

1. Update the root `package.json` with your repository name and url.

2. Modify the sample packages as needed and remember to update their `package.json`.

   > **NOTE:** For a package to be releasable to GitHub Package Registry, it must be scoped to match the owner of the repository. The package name is optional, as long as it is unique under that scope. In addition, the `repository.url` field needs to be consistent in all package.json files.

3. Run `yarn bootstrap` to bootstrap the packages. This will install all of their dependencies and links any cross-dependencies.

## How it works

Each push to `master` branch will generate a version number, git tag, Conventional Changelog, release commit, pushing changes to the origin and publish to GitHub Package Registry.

## Protected branches

If you're using the protected branches feature, you'll need a Personal Access Token because the `GITHUB_TOKEN` generate by the CI won't have enough permission (that's by design). You can generate one in your [account settings](https://github.com/settings/tokens) and set it in the repository secrets.

You'll also need to modify your action to:

- Use `persist-credentials: false` when checking out the branch;
- Set the repository remote to https format with the newly generated token.


```yml
# ...
            - uses: actions/checkout@v3
              with:
                  persist-credentials: false
                  fetch-depth: 0
# ...
          - name: Config git user
              run: |
                  git config --global user.name "${{ github.actor }}"
                  git config --global user.email "${{ github.actor }}@users.noreply.github.com"
                  git remote set-url origin https://${{ github.actor }}:${{ secrets.PERSONAL_ACCESS_TOKEN }}@github.com/${{ github.repository }}
# ...
```
