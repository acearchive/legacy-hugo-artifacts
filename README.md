![Unmaintained](https://img.shields.io/badge/unmaintained-%F0%9F%9B%87-red?style=for-the-badge)

**DEPRECATED**

*This repo has been deprecated now that we are no longer using IPFS for hosting
content. The documentation below is no longer accurate. See
[artifact-submissions](https://github.com/acearchive/artifact-submissions) and
[hugo-artifacts](https://github.com/acearchive/hugo-artifacts) instead.*

# artifacts

This repository contains metadata for all the artifacts in [Ace
Archive](https://acearchive.lgbt).

For every artifact in the archive, there is an *artifact file* in this repo. An
artifact file holds metadata about the artifact, including
[CIDs](https://docs.ipfs.io/concepts/content-addressing/) of files associated
with it.

Each artifact file is a markdown document containing a YAML front matter block,
however no content goes in the body of the markdown file, so you can just think
of it as a YAML file with a leading and trailing `---` line and a `.md` file
extension. The reason why markdown files are used over plain YAML files is for
compatibility with [Hugo](https://gohugo.io/), the static site generator we use
to build the site. Currently, Hugo [does not
support](https://github.com/gohugoio/hugo/issues/5074) generating pages from
YAML/JSON/TOML files.

The file name of each artifact file (sans file extension) is the URL slug of
the artifact on the site. If the URL slug of an artifact needs to change for
any reason, rename the file in this repo and add the old URL slug to the
`aliases` field.

[The schema of artifact files is documented
here.](https://acearchive.lgbt/docs/contributing/artifact-files/)

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
[CID](https://docs.ipfs.io/concepts/content-addressing/). You can do this in
one of two ways:

- You can use an IPFS implementation like
  [go-ipfs](https://github.com/ipfs/go-ipfs) or
  [js-ipfs](https://github.com/ipfs/js-ipfs).
- You can use HTTP via an [IPFS
  gateway](https://docs.ipfs.io/concepts/ipfs-gateway/) like `dweb.link`.

## Hosting

The content of the archive is hosted on the IPFS network using
[Web3.Storage](https://web3.storage). We use GitHub Actions workflows to
automatically validate the syntax of artifact files when a pull request is
opened and upload the content to Web3.Storage when a pull request is merged.
The code which does this can be found at
[acearchive/artifact-action](https://github.com/acearchive/artifact-action).

## Schema version

Artifact files have a schema version specified by a top-level `version` field,
which is an integer that starts at `1` and increments with each
backwards-incompatible change to the schema of artifact files.

Whenever there's a schema version bump, all artifacts in this repo will be
migrated to the new version. This means that all artifact files in the tip of
`main` should always have the latest schema version.

The reason for embedding the schema version in the artifact file is that
[acearchive/artifact-action](https://github.com/acearchive/artifact-action) can
be used to retrieve previous versions of artifact files as well as the current
version.

You can see a changelog of all artifact file schema versions at
[CHANGELOG.md](./CHANGELOG.md).

## Example

This is an example of an artifact file.

```yaml
---
version: 2
title: "*The Asexual Manifesto*"
description: >
  A paper by the Asexual Caucus of the New York Radical Feminists
files:
  - name: "Digital Scan"
    mediaType: "application/pdf"
    filename: "the-asexual-manifesto.pdf"
    cid: "bafybeihsf4562gmmyoya7eh5buxv65lqcdoil3wsi5jf5fceskap7yzooi"
  - name: "Transcript"
    mediaType: "text/html"
    cid: "bafybeiakup4b3mjmzw7mjq3ptnv3dqusdebskra2jic73u74nhbizgu3wi"
links:
  - name: "Internet Archive"
    url: "https://archive.org/details/asexualmanifestolisaorlando"
people: ["Lisa Orlando", "Barbara Getz"]
identities: ["asexual"]
fromYear: 1972
decades: [1970]
---
```
