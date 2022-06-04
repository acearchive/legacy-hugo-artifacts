# artifacts

This repository contains all the [artifact
files](https://acearchive.lgbt/docs/contributing/artifact-files/) for [Ace
Archive](https://acearchive.lgbt). These files contain the metadata for
artifacts in the repository, and they're used to build the site.

## Contributing

If you would like to contribute an artifact to Ace Archive, see [the
contributing
documentation](https://acearchive.lgbt/docs/contributing/getting-started/).
While you are of course welcome to write an artifact file by hand and open a PR
directly, it is recommended that you use [this
form](https://acearchive.lgbt/new-artifact/) instead because it performs input
validation and does some magic to normalize CIDs.

## API

Ace Archive does not provide a REST API because rather than using a centralized
database, artifact metadata is just checked into this repository and artifact
content is publicly available on the IPFS network. Instead, we provide a CLI
tool and a GitHub Action at
[acearchive/artifact-action](https://github.com/acearchive/artifact-action)
that can parse the files in this repository and return the artifact metadata as
JSON. Since artifact metadata is version-controlled with git, you can query
both the current and previous versions of artifacts.

Once you have an artifact's metadata, you can query the files associated with
that artifact by the file's
[CID](https://docs.ipfs.io/concepts/content-addressing/#identifier-formats).
You can do this in one of two ways:

- You can use an IPFS implementation like
  [go-ipfs](https://github.com/ipfs/go-ipfs) or
  [js-ipfs](https://github.com/ipfs/js-ipfs).
- You can use HTTP via an [IPFS
  gateway](https://docs.ipfs.io/concepts/ipfs-gateway/) like `dweb.link`.

## Hosting

The content of the archive is hosted on the IPFS network using
[Web3.Storage](https://web3.storage). We use GitHub Actions workflows to
automatically validate the syntax of [artifact
files](https://acearchive.lgbt/docs/contributing/artifact-files/) when a pull
request is opened and upload the content to Web3.Storage when a pull request is
merged. The code which does this can be found at
[acearchive/artifact-action](https://github.com/acearchive/artifact-action).
