# artifacts

This repository contains all the [artifact
files](https://acearchive.lgbt/docs/contributing/artifact-files/) for [Ace
Archive](https://acearchive.lgbt). These files contain the metadata for
artifacts in the repository, and they're used to build the site.

If you would like to contribute an artifact to Ace Archive, see [the
contributing
documentation](https://acearchive.lgbt/docs/contributing/getting-started/).
While you are of course welcome to write an artifact file by hand and open a PR
directly, it is recommended that you use [this
form](https://acearchive.lgbt/new-artifact/) instead because it performs input
validation and does some magic to normalize CIDs.

## API

Ace Archive does not provide a traditional REST API because artifact metadata
is just checked into this repository and artifact content is publicly available
on the IPFS network. However, we do provide both a CLI tool and a GitHub Action
at [acearchive/artifact-action](https://github.com/acearchive/artifact-action)
that can parse the files in this repository export the data as JSON.

## Hosting

The content of the archive is hosted on the IPFS network using
[Web3.Storage](https://web3.storage). We use GitHub Actions workflows to
automatically validate the syntax of [artifact
files](https://acearchive.lgbt/docs/contributing/artifact-files/) when a pull
request is opened and upload the content to Web3.Storage when a pull request is
merged. The code which does this can be found at
[acearchive/artifact-action](https://github.com/acearchive/artifact-action).
