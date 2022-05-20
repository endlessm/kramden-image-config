# Endless OS 4.0 – Kramden Institute Configuration 

Configuration for Endless OS 4.0 deployment at [Kramden Institute] to be used
with [eos-image-builder].

## Using

Clone this repository and [eos-image-builder]:

```bash
git clone https://github.com/endlessm/eos-image-builder.git
git clone https://github.com/endlessm/kramden-image-config.git
```

Check out the stable branch of eos-image-builder (currently `eos4.0`):

```bash
git -C eos-image-builder checkout eos4.0
```

Run the image builder as follows:

```bash
sudo ./eos-image-builder/eos-image-builder \
    --localdir ./kramden-image-config \
    --personality kramden \
    --use-production-ostree \
    eos4.0
```

The parameters have the following meanings:

| Parameter(s) | Meaning |
| ------------ | ------- |
| `--localdir ./kramden-image-config` | Load additional configuration from this repository |
| `--personality kramden` | Build the `kramden` image personality defined in this repository, rather than the default (`base`) |
| `--use-production-ostree` | Use a released version of Endless OS, rather than a nightly build |
| `eos4.0` | Use the `eos4.0` branch of Endless OS, rather than the development branch (`master`) |


When the image has been successfully built, the output can be found in
`/var/cache/eos-image-builder/tmp/`.

## Components

The main functionality of the image builder lives in [eos-image-builder].
This repository provides specific configuration for use by [Kramden Institute].

* `config` - The INI files containing the settings for each build. These
  are loaded after those from eos-image-builder and can build on them
  using the same rules defined there.

* `data` - Data files used for Endless images. To refer to them in
  configuration, use `${build:localdatadir}`. To refer to them from
  hooks, use `${EIB_LOCALDATADIR}`.

* `hooks` - Scripts and snippets run during the image build stages. See
  the documentation in eos-image-builder for the available hook stages.
  If a hook in this repository and the [eos-image-builder] repository have the
  same name, the hook in this repository is used.

* `lib` - Python modules to be loaded from hooks. Typically hooks are
  self contained, but occasionally a separate module can be used for
  encapsulation or code sharing. This path is added at the beginning of
  `PYTHONPATH`, so modules from this directory are preferred to those in
  eos-image-builder.

[Kramden Institute]: https://kramden.org/
[eos-image-builder]: https://github.com/endlessm/eos-image-builder/
