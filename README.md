heroku-buildpack-vips
=====================

[![Vips 8.17.3](https://img.shields.io/badge/vips-8.17.3-blue)](https://github.com/Newlywords/heroku-buildpack-vips/releases)
[![Heroku 22](https://img.shields.io/badge/stack-22-904edf?logo=heroku)](https://github.com/Newlywords/heroku-buildpack-vips/releases)
[![Heroku 24](https://img.shields.io/badge/stack-24-904edf?logo=heroku)](https://github.com/Newlywords/heroku-buildpack-vips/releases)

## Disclaimer

If you don't need the `vips` binary, and you also don't need the latest version of vips, you might not need this
buildpack. Take a look [here](https://devcenter.heroku.com/articles/stack-packages) at the versions that are now
included in the Heroku stacks by default.

There are some known security issues with using outdated versions, see [this issue
comment](https://github.com/Newlywords/heroku-buildpack-vips/issues/36#issuecomment-1644417628) for more information.

## Important changes

The brief usage of pdfium that started August 2023 ended September 17, 2023. The buildpack is using poppler again due
to https://github.com/Newlywords/heroku-buildpack-vips/issues/41#issuecomment-1722462354.

## Dependencies

This buildpack includes all necessary runtime dependencies. The following libraries are bundled from source when not available in the stack:

**heroku-22:**
- libarchive 3.6.0

**heroku-24:**
- libgsf 1.14.53
- liborc 0.4.32

Found out more information like this in [the changelog](CHANGES.md).

## About this buildpack

A VIPS buildpack for the modern Heroku stacks. This stack supports the following
stacks:

- heroku-22
- heroku-24

If you have problems on any of these stacks, or if a new stack comes out that is
unsupported, please file an issue.

If you would like to use a build for a deprecated stack, the last versions which supported deprecated stacks
are tagged with the stack name.

Important notes:

This buildpack started out as one of the many that are out there, and ended up
being completely different. The build script uses docker and also includes pdf
support via poppler.

Additionally, if you are planning to use [sharp](https://github.com/lovell/sharp), you may also need the following packages:
- libheif-dev
- libfftw3-dev
- libwebp-dev

The easiest way to do this is using the [heroku apt buildpack](https://github.com/heroku/heroku-buildpack-apt).

This buildpack was put together with the help of John Cupitt, the creator of
libvips. He was invaluable in my efforts to get a working libvips installation
with pdf support on heroku. Thank you John!

---

Heroku buildpack with [libvips](https://github.com/libvips/libvips) installed.


## Usage

Add this buildpack by running:

```
heroku buildpacks:add https://github.com/Newlywords/heroku-buildpack-vips
```

After running this command you should see the output similar to:

```
Buildpack added. Next release on amazing-earthfest will use:
  1. heroku/ruby
  2. https://github.com/Newlywords/heroku-buildpack-vips
```

## Build script

[This](./build.sh) is the script used to build vips using docker.

```sh
VIPS_VERSION=x.y.z ./build.sh
```

After building a tar file, it will be copied to the `build` directory. Then you should commit this changes to git.

## Build configurations

If you would like to see the output of `vips --vips-version` or `vips --vips-config`, both can be found for each stack
in the [build/configurations](build/configurations) directory. These configuration logs are generated automatically
during the build process, so they should always be up-to-date.
