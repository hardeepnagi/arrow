# How to manage several repositories

## Searching

Find some combinations of search qualifiers:

* [Repositories of **arrow-kt** organization (sorted by update): `org:arrow-kt sort:updated`](https://github.com/search?q=org%3Aarrow-kt+sort%3Aupdated)
* [Open pull requests of **arrow-kt** organization (sorted by update): `org:arrow-kt is:pr is:open sort:updated`](https://github.com/search?q=org%3Aarrow-kt+is%3Apr+is%3Aopen+sort%3Aupdated)
* [Open issues of **arrow-kt** organization (sorted by update): `org:arrow-kt is:issue is:open sort:updated`](https://github.com/search?q=org%3Aarrow-kt+is%3Aissue+is%3Aopen+sort%3Aupdated&type=Issues)

## Gradle tasks

One of the drawbacks of multi-repo is the ability to check changes that could impact on other repositories.

In order to overcome that situation, new Gradle tasks are provided for every repository:

```
$> ./gradlew tasks

...

------------------------------------------------------------
Tasks runnable from root project
------------------------------------------------------------

Arrow tasks
-----------
buildArrowProject - Build with local Arrow dependencies (tests execution included)
buildArrowProjects - Build libs and examples with local Arrow dependencies (tests execution included)
installArrowLibs - Install all the artifacts using local Arrow dependencies (no tests execution)

Arrow (Git) tasks
-----------------
gitPull - Run git-pull for all the repositories
gitPullOthers - Run git-pull for the rest of the repositories
```

## Other tools

Find some scripts to download all the new repositories in [`utils`](utils/) directory.
