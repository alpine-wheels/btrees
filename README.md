# Alpine Wheels template repository

Use this repository as a starting point for a new package that you want to include in the Alpine Wheels package index.

### Usage

1. Update `requirements.txt` with the package name and version of the package you want to build.  
   **Do not** include more than one package in `requirements.txt`.
2. Update `build.sh` to include any OS packages that are required for the package to build.
3. Update `.github/workflows/build-wheel.yaml` with the image tags for the versions of Python you want to build wheels 
   for.
4. Run `IMAGE_TAG=3.11-alpine docker compose run --rm --no-TTY build` to verify that the package builds correctly.
   Test with any value of `IMAGE_TAG` that you want to build a wheel for.
5. You can also add additional platforms (e.g. linux/arm64) to `.github/workflows/build-wheel.yaml` if you want to build
   wheels for platforms other than linux/amd64.

If everything went well, there will be a single `*.whl` file in the repository directory. **Do not** commit this file.

Commit your changes to `requirements.txt`, `build.sh`, and `.github/workflows/build-wheel.yaml`. When any changes are
pushed to the `master` branch, the workflow in this repository will run the build script.

### Releases

When you are confident the build works as expected, create a new release. The tag and release title should both be the
version number for this release.

After publishing the release, the workflow in this repository will build the wheel file and upload it to the release. It
will also send information about the release to the repository at [alpine-wheels/index][a].

[a]: https://github.com/alpine-wheels/index
