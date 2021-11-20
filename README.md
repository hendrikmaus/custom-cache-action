# Custom Cache Action

A custom caching mechanism that uses a container registry to save and restore a tarball for a cache.

This action does not utilize GitHub Actions' native `cache` system on purpose. The custom mechanism allows for implementing caching on GitHub Releases (i.e. `git tag`'s), which the native `cache` cannot do.

*Please find [the blog post](https://blog.hendrikmaus.dev/github-actions-release-caching/) I wrote on the topic.*
