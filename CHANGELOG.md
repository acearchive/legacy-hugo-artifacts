# Changelog

This is a changelog for changes to the artifact file schema version.

## Version 1

This is the initial version.

## Version 2

Previously, `title`, `description`, and `longDescription` accepted HTML for
inline markup. With this version, they now use markdown instead.

# Version 3

Previously, the `filename` field of `files` was optional. Now, it is mandatory.
Additionally, now file names are required to be unique within the same
artifact.
