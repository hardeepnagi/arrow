# How it works

**arrow** repository orchestrates all the Λrrow libraries.

## Configuration

| File | Description | Comment |
| ---- | ----------- | ------- |
| [`gradle.properties`](https://github.com/arrow-kt/arrow/blob/master/gradle.properties) | Global properties | Every library loads these properties when starting a Gradle execution. |
| [`generic-conf.gradle`](https://github.com/arrow-kt/arrow/blob/master/generic-conf.gradle) | Global build configuration | Every library loads this configuration when starting a Gradle execution. **Note**: it shouldn't include particular configuration for a library. For instance, `arrow-benchmarks-fx` adds JitPack.io repository in its `build.gradle`. |
| [`subproject-conf.gradle`](https://github.com/arrow-kt/arrow/blob/master/subproject-conf.gradle) | Global sub-project build configuration | Every library loads this configuration when starting a Gradle sub-project execution. |
| [`doc-conf.gradle`](https://github.com/arrow-kt/arrow/blob/master/doc-conf.gradle) | Configuration to build and check the documentation | This file is loaded for those libraries that generate documentation. |
| [`publish-conf.gradle`](https://github.com/arrow-kt/arrow/blob/master/publish-conf.gradle) | Configuration to publish a library | This file is loaded for those libraries that must be published in artifact repositories. |

If these files are changed, a full check for all the libraries will be executed to approve the pull request.

## Build order

It's necessary to keep a [build order](../../lists/build.txt) according to the dependencies among libraries.

That order is used when doing full checks for all the Λrrow libraries. In those checks, external Λrrow dependencies for a library come from the **local** repository.

If this file is changed, a full check for all the libraries will be executed to approve the pull request.

## Checks

Every library has these checks:

* On **pull request** (external Λrrow dependencies come from OSS repository):
    * Build library.
    * Build and check the documentation.

* On **pushing changes** to `master` branch (an issue will be created in case of failure):
    * Publish library in OSS repository.
    * Publish documentation for the `next` version (just apidocs for that library).
    * **Full build check** for all the libraries (external Λrrow dependencies come from **local** repository).
    * **Full doc check** for all the libraries (external Λrrow dependencies come from **local** repository).

Those checks just call the commands included in the [`scripts`](../../scripts) directory.

If these files are changed, a full check for all the libraries will be executed to approve the pull request.

## Release

Every Arrow library publishes SNAPSHOT versions from its repository. However, RELEASE versions mush be published at the same time.

In order to publish a RELEASE version, prepare a pull request for `arrow` repository with these changes:

* Update versions in `gradle.properties`. For instance, the release version will be `0.10.5` and the next SNAPSHOT version will be `0.11.0-SNAPSHOT`:
```
VERSION_NAME=0.11.0-SNAPSHOT
LATEST_VERSION=0.10.5
```
* Update versions in `README.md`

When merging that pull request:

* New RELEASE version will be published into Bintray for all the Arrow libraries.
* A first SNAPSHOT version will be published into OSS for all the Arrow libraries (because they depend on SNAPSHOT versions for other Arrow libraries by default).
* Documentation website will be updated as well.

Then, it will be necessary to sync Bintray with Maven (pending task: automating it).
