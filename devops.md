# DevOps


### Git Tags
`git tag -a v1.0.0 -m "Releasing version 1.0.0"`
* lightweight tags are just a bookmark for a commit 
*  

#### Semantic Versioning
* `MAJOR.MINOR.PATCH`
* minor are backwards compatible 
* major are breaking changes 


### GitHub Workflow

#### Publishing a Rust Crate
To nicely publish a rust binary, there are a couple of things that you want to do:

Manual Steps:
1. Tag the release
2. Update the `Cargo.toml` 

Workflow Steps:
3. Build the package
4. Publish on GitHub
5. Publish on crates.io

### Workflow file
```yaml
name: Github Release

on:
  push:
    tags:

      - 'v[0-9]+.[0-9]+.[0-9]+'

jobs:
  test:
    uses: ./.github/workflows/integration.yml
  release:
    name: Github Release
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v2
      - name: Toolchain
        uses: actions-rs/toolchain@v1
        with:
          profile: minimal
          toolchain: stable
          override: true
      - name: Build Release
        uses: actions-rs/cargo@v1
        with:
          command: build
          args: --release
      - name: Publish Release
        uses: softprops/action-gh-release@v1
        with:
          files: target/release/gci
      - name: Publish Crate
        run: cargo publish --token ${CARGO_REGISTRY_TOKEN}
        env:
          CARGO_REGISTRY_TOKEN: ${{ secrets.CARGO_REGISTRY_TOKEN }}

```

1. Tag the release 
   - on a branch (`main` or `release/<semver-without-patch>`) tag the latest commit with the semver.
   ```shell
   git tag -a <semver-tag> -m "Releasing <semver-tag>"
   ```

2. Update the version in the `Cargo.toml`

3. Push the tag to GitHub 
   ```shell
   git push origin <semver-tag> 
   ```
   
Once the tag has been pushed, the workflow will run on GitHub. 
