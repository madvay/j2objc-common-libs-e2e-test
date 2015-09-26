Please keep in mind that your "Contribution(s)" are submitted under
the [Apache 2.0 License](LICENSE).

#### Updating j2objc-gradle
The version of j2objc-gradle in this repo is not automatically kept up
to date with master of https://github.com/j2objc-contrib/j2objc-gradle.

As a submodule, you can update j2objc-gradle by doing:

```shell
# (start with a clean git working directory)
# (from your local repo for this project)
git checkout -b update-plugin
pushd j2objc-gradle
git pull
popd
git add .
git commit -m 'Updating j2objc-gradle to HEAD'
# (submit the update-plugin branch as a PR to the repo)
```

Make sure this PR is seperate from any other work.  If a library you want
to build depends on the update, work in a new branch parented to the commit
above.

#### Library build verification

On OS X we have system tests under the `libraryBuilds` directory.  Each test directory
has one root Gradle project (and zero or more subprojects), some or all of which apply the
`j2objc-gradle` plugin.  Locally you can run them as follows:

```sh
# Once per git repository and/or new release of j2objc, run prep.
pushd libraryBuilds && ./prep.sh && popd
# This downloads j2objc and prepares the environment.

# Every time you want to run the build tests:
./gradlew build && pushd systemTests && ./run-all.sh && popd
# Normal Gradle build results will be displayed for each test project.
```

These system tests are also run as part of OS X continuous integration builds on Travis.
You are not required to run the system tests locally before creating a PR (they can take
time and processing power), however if the tests fail on Travis you will need to update
the PR until they pass.

When you add a new library to build, make sure it is referenced in run-all.sh (for
human contributors) and in .travis.yml (for continuous builds).
