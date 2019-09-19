# These are example snippets and BUILD files for [Bazel](https://github.com/bazelbuild/bazel).

Example with a Codefresh pipeline

```yaml
version: "1.0"
stages:
  - "clone"
  - "build"
steps:
  main_clone:
    type: "git-clone"
    description: "Cloning main repository..."
    repo: "todaywasawesome/bazelbuild-examples"
    revision: "${{CF_BRANCH}}"
    stage: "clone"
  bazel_beforecache:
    image: iankoulski/tree
    commands:
    - tree ${{CF_VOLUME_PATH}}
  bazel_build:
    stage: "build"
    image: gcr.io/cloud-marketplace-containers/google/bazel:0.29.1
    commands:
    - cd java-tutorial && bazel build //:ProjectRunner
  bazel_cache:
    image: iankoulski/tree
    commands:
    - tree ${{CF_VOLUME_PATH}}
    ```
