# Setup Spack in Github Actions

Set up the [Spack package manager](https://github.com/spack/spack).

Example usage:

```yaml
jobs:
  build:
    runs-on: ${{ matrix.os }}

    strategy:
      fail-fast: false
      matrix:
        os:
        - ubuntu-18.04
        - ubuntu-20.04
        - macos-10.15
        concretizer:
        - original
        - clingo

    steps:
      - uses: actions/checkout@v1.0.0
      - name: Set up Spack
        uses: haampie-spack/setup-spack@v1
        with:
          os: ${{ matrix.os }}
          concretizer: ${{ matrix.concretizer }}
          ref: develop
      - run: |
        spack --version
        spack install zlib
```

## Speeding up the builds

If you want fast builds make sure to:

- Fix spack itself on a particular commit (e.g. set `ref: [commit sha]`);
- Build environments and use the lock file as the hash key (I'll add an example soon).


## How is Spack bootstrapped?

This environment is built

https://github.com/haampie-spack/setup-spack/blob/rebuild-spack/spack.yaml

and the binaries are uploaded as release assets to

https://github.com/haampie-spack/setup-spack/releases/tag/develop

Todo:
- [ ] Add checksum verification
- [ ] Add caching example
