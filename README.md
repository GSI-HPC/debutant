Debutant is a Debian package building framework for
- proprietary software that is shipped as binary only
- and where redistribution is normally prohibited

This software is work in progess!

# Rationale

Normally automatic package transformation is done by alien. 
Anyhow aliens fully-automatic conversion does not always lead 
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

# Usage

Available recipes are in the recipes/ subdir.

`debutant _recipe_ [ _additional arguments_ ]` runs the given recipe and 
tries to build the package.
