# dotnet-repo-template

A template repository meant to be used for solutions intended
to be published to nuget.

## Directory Structure

```
./
|-- .github/
  |-- workflows/
|-- src/
  |-- RenameMe.sln
  |-- tests/
```

_Don't forget to rename the solution file before creating projects_

## GitVersion

Git version is supported out of the box with a relatively simple configuration
which can be found in the [GitVersion](GitVersion.yml) file.

## Git Ignore

The `.git ignore` file is tailored for _dotnet_ projects and includs ignores for
`.idea/` (JetBrains) and `.DS_Store/` (OSx) folders. Depending on the use case
the `.gitignore` file may need to be updated.

## License, Copyright

A license file for `MIT` is included. The default copyright is for
__Oneirosoft__ and can be updated as needed.

_Check the date as it may need to be updated accordinly_.

## Workflows

Included are workflows for:

- ci
- ci-pr
- publish

These templates are located in `.github/workflows`.

__ci__

The `ci` workflow will build and test all projects in the solution when
an update to main or a tag starting with `v*` is pushed or merged.

The tests use MSTest Adaptor and will need to be modified when using Microsoft's
Testing Platform.

__ci-pr__

The `ci-pr` workflow will build and run for any pull request. 

The tests use MSTest Adaptor and will need to be modified when using Microsoft's
Testing Platform.

__publish__

Publish will publish all packable projects contained in the soltuion and relies
on a `NUGET_API_KEY` to be present for the workflow. All projects will be built
and tested before being packed and published to nuget.org.

The tests use MSTest Adaptor and will need to be modified when using Microsoft's
Testing Platform.

## Tests

A sample unit test project has been included and should be renamed appropriately.
The unit tests should be placed in `src/tests/`.

_The `placeholder.txt` file can be safely removed and is only
there for git_
