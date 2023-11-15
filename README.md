# haskell-dev-tools

_copied from fossas/haskell-dev-tools_

This repo serves two purposes:

- Creating the docker image that is used to run the linter and formatter in
  the CI builds for my haskell projects.
- Automatically creating PRs for the image when the tools are updated.

Most of this repo is in the `.github/workflows` folder, but the two special
items are the Dockerfile, and the script that updates it: `update-dev-tools.sh`.

The image that is built is scoped to this repo as well as the org, but is made
publicly available, since there's no secrets or magic, and it makes docker auth
easier in spectrometer's CI. On that note, the code in this repo is released
warranty-free into the public domain, under [The Unlicense](LICENSE).

The image is published as `ghcr.io/kwest-ng/haskell-dev-tools:{version}-{hash}`, where
`version` is the GHC compiler version we target, and `hash` is the git hash of the
commit used to build the image.

## Updating the container

### How to update the version of a tool in the container

Don't.  This repo automatically updates tools to their latest versions, and
will override ANY version change in the dockerfile.

### How to add a new tool to the container

Update the `update-dev-tools.sh` file and add the tool you're interested in.
Then, add it to the install command in the dockerfile.  Match the format of
the existing tools.

You can enable auto-merge on your PR, and it will automatically publish to
the container registry after about 1 hour (due to long build times).

Once it's published, you can use it immediately.
