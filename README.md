# Endless OS 4.0 – Kramden Institute Configuration 

Configuration for Endless OS 4.0 deployment at [Kramden Institute] to be used
with [eos-image-builder].

## Using

To use the configuration here, pass the path to this checkout in the
`--localdir` option to [eos-image-builder]. For instance:

```
git clone https://github.com/endlessm/eos-image-builder.git
./eos-image-builder/eos-image-builder --localdir .
```

## Components

The main functionality of the image builder lives in [eos-image-builder].
This repo provides specific configuratoin for use by [Kramden Institute].

* `config` - The INI files containing the settings for each build. These
  are loaded after those from eos-image-builder and can build on them
  using the same rules defined there.

* `data` - Data files used for Endless images. To refer to them in
  configuration, use `${build:localdatadir}`. To refer to them from
  hooks, use `${EIB_LOCALDATADIR}`.

* `hooks` - Scripts and snippets run during the image build stages. See
  the documentation in eos-image-builder for the available hook stages.
  Hooks from this repository are preferred if they are named identically
  to those in eos-image-builder.

* `lib` - Python modules to be loaded from hooks. Typically hooks are
  self contained, but occasionally a separate module can be used for
  encapsulation or code sharing. This path is added at the beginning of
  `PYTHONPATH`, so modules from this directory are preferred to those in
  eos-image-builder.

[Kramden Institute]: https://kramden.org/
[eos-image-builder]: https://github.com/endlessm/eos-image-builder/
