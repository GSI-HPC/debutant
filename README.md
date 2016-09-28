Debutant is a framework for creating Debian packages for
- proprietary software that is shipped as an arbitrary binary blob
- and where redistribution is normaly prohibited

Packaging is done by individual 'recipes'.

This software is work in progess! For now it is implemented as a bash script.

# Requirements

To make effective use of debutant you need to have the standard packaging toolset installed:

- dh-make
- devscripts + recommends
- debhelper
- dpkg-dev + recommends

# Usage

`./debutant` lists the available recipes.

`debutant _recipe_ [ _recipe specific arguments_ ]` runs the given recipe and
builds the package.

# Writing recipes

Create a file called `recipe` in a folder `./recipes/_foo_`.
At first debutant creates a temporary $BUILD_DIR where all action takes place.

Basic skeleton:
```bash
ARCHIVE=`fetch _URL_` # downloads the blob to $BUILD_DIR

extract $ARCHIVE      # unpack blob

# this dir will be used in the nect steps:
PKG_DIR=_dir where $ARCHIVE was extracted to_

debut_dh_make         # create debian/… for packaging

# packaging refinements ...

build_package         # runs debuild

# copy back results from $BUILD_DIR to the current directory
drop_result
```

## Additional commands:

Normal debian packaging files (eg. `install`, `rules` etc.) can be put in a
./recipes/_foo_/debian/` folder and added with `add_debian_files`.

Entries in `debian/control` may be changes with `debian_control`

Dependencies can be added with `add_dependency`

For further information take a look at the source and the available recipes.

# Rationale

Normally automatic package transformation for Debian-based distros is done
by alien.
Anyhow alien's fully-automatic conversion does not always lead
to satisfying results esp. for mass deployments, e.g.
- packages want to install to /usr/local or /opt
- postinst et al does nasty things
  eg. drop tarballs that are never cleaned up or remove files
  that don't belong to the package
- debian/control has to be tweaked eg. to include the proper dependencies

Therefore alien-created packages normally need some manual modifications
that have to be redone for every new software version.

This leads to the fact that many specific workarounds exist to install
non-free but publicly available software, like
- flashplugin-nonfree
- java-package,
- sapgui-package
- ttf-mscorefonts-installer

Debutant aims to circumvent these issues by providing some wrappper functions
and recipes that automatically transform the software into Debian packages
that conform to the Debian standards as good as possible.

This provides the chance to improve the quality of proprietary binary blobs by
applying the debian quality assurance tool chain eg. lintian.
