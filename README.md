# Pandoc Buildpack

A Heroku buildpack for [pandoc](http://pandoc.org).

### Installation

To install this buildpack run:
```
$ heroku buildpacks:add https://github.com/scholastica/pandoc-buildpack.git -a [YOUR-APP-NAME]
```

OR use a [tagged version](https://github.com/scholastica/pandoc-buildpack/releases)

```
$ heroku buildpacks:add https://github.com/scholastica/pandoc-buildpack.git#2.0.3 -a [YOUR-APP-NAME]
```

The buildpack will be installed on the next heroku deploy.


### What It Does

* The buildpack script downloads a prebuilt debian archive
from the [pandoc repository](https://github.com/jgm/pandoc/releases).
    * If the deb archive already exists in the heroku buildpack cache, the cached
    version will be used instead.
* The script then extracts the `pandoc` binary from this archive into `/app/vendor/pandoc/bin`.
* Finally, the script adds `/app/vendor/pandoc/bin` to the `PATH`.

For details, see the script in [bin/compile](,/bin/compile).
