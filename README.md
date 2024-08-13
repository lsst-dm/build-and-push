
  This composite action builds a Docker image, tags it with the current git
  branch/tag and if is the main branch it also tags it with latest.
  Finally pushes it to ghcr.io but could push to docker.

## Usage

```yaml
name: CI

"on":
    push:
        branch:
        - main
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - uses: lsst-dm/build-and-push@main
        id: build
        with:
            github_token: ${{ secrets.GITHUB_TOKEN }}

```
## Inputs

-  `github_token` (string, required) "The GitHub token to use for authentication."
-  `docker_token` (string, optional) "The Docker token to use for authentication."
-  `image` (string, optional) "The name of the Docker image to build."
-  `dockerfile` (string, optional) "The name of the Dockerfile to build."
-  `context` (string, optional) "The build context to use."
-  `push` (boolean, optional) "Whether to push the image to ghcr.io."
-  `platforms` (list, optional) "List of target platforms for build"
-  `tags` (list, optional) "List of tags using events from docker/metadata-action"
-  `build-args` (list, optional)

## Outputs
- `tag` (string) the tag of the image that was pushed.


#### Inspired by https://github.com/lsst-sqre/build-and-push-to-ghcr
