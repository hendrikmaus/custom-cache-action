# Custom Cache Action

A custom caching mechanism that uses a container registry to save and restore a tarball for a cache.

This action does not utilize GitHub Actions' native `cache` system on purpose. The custom mechanism allows for implementing caching on GitHub Releases (i.e. `git tag`'s), which the native `cache` cannot do.

*Please find [the blog post](https://blog.hendrikmaus.dev/github-actions-release-caching/) I wrote on the topic.*

## Usage

Make sure to authenticate to the container registry that you want to use to store the cache image, e.g. GitHub Packages:

```yaml
- name: Log in to the Container registry
  uses: docker/login-action@v1
  with:
    registry: 'ghcr.io'
    username: ${{ github.actor }}
    password: ${{ secrets.GITHUB_TOKEN }}
```

Then try to **restore an existing cache** image:

```yaml
- name: Restore cache
  uses: hendrikmaus/custom-cache-action/restore@master
  with:
    registry: 'ghcr.io'
    image: 'owner/repository'
    tag: 'cache-latest'
```

After work is done, **save a cache** and push it:

```yaml
- name: Save cache
  uses: hendrikmaus/custom-cache-action/save@master
  with:
    paths: "${{ github.workspace }}/something /path/to/something/else"
    registry: 'ghcr.io'
    image: 'owner/repository'
    tag: 'cache-latest'
```
