# Building Hello-IT

To prepare a new Hello-IT release, some steps must be followed in a specific order.

## Preparation

General code submission follows the git flow pattern. 

Once `develop` branch is ready for a new version, a new `release` branch named with the version number only (no `v` first).

## Building the release

To build the release once in the release branch, use the `BuildAndPackage.command` script.

By default, build script will look for the Developer ID Installer named `Developer ID Installer: Yoann GINI (CRXPBZF3N4)`. Use `CUSTOM_DEVELOPER_ID_INSTALLER` environmental variable to specify your own.

The script will build the app with all dependencies in the right order, sign it, create the package, and sign it too.

The script will build the app in `Release` config when the current branch is under `release` or is `master`. All other branches will be built in `Debug` config.

App version will be grabbed from git branches name or let untouched if the branch name does not match the pattern `release/version`. If version number is updated, it will automatically be committed before building the release.

Build version is generated from the number of git commits in the history from the current branch point of view.

Once built and tested, and only for final release (not for beta), the release branch must be merged in the master tree. Last commit to merge should be the one updating the app version. Returning to this exact commit will allow a developer to recreate the app in the exact same states (and so build version will be the same).

The build will deny to start if there is some uncommitted change to the repo.

## Distribution

The pkg created at the previous step can now be updated into the Github Release system with a nice description and the pkg as the only payload.