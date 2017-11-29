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

### Release Instructions

To cut a new release use
the [github user interface](./pandoc-buildpack/releases).

<img width="1039" alt="screen shot 2017-11-29 at 7 49 38 am" src="https://user-images.githubusercontent.com/72979/33378366-2cf43714-d4da-11e7-9f87-f4f472206388.png">



### What It Does

* The buildpack script downloads a prebuilt debian archive
from the [pandoc repository](https://github.com/jgm/pandoc/releases).
    * If the deb archive already exists in the heroku buildpack cache, the cached
    version will be used instead.
* The script then extracts the `pandoc` binary from this archive into `/app/vendor/pandoc/bin`.
* Finally, the script adds `/app/vendor/pandoc/bin` to the `PATH`.

For details, see the script in [bin/compile](,/bin/compile).
