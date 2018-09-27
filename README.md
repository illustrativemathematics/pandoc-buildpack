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
the [github user interface](https://github.com/scholastica/pandoc-buildpack/releases).

<img width="1039" alt="screen shot 2017-11-29 at 7 49 38 am" src="https://user-images.githubusercontent.com/72979/33378366-2cf43714-d4da-11e7-9f87-f4f472206388.png">


### What It Does
* The buildpack script downloads a prebuilt debian archive
from the [pandoc repository](https://github.com/jgm/pandoc/releases).
    * If the deb archive already exists in the heroku buildpack cache, the cached
    version will be used instead.
* The script then extracts the `pandoc` binary from this archive into `/app/vendor/pandoc/bin`.
* Finally, the script adds `/app/vendor/pandoc/bin` to the `PATH`.

For details, see the script in [bin/compile](,/bin/compile).


## How to upgrade Pandoc version

#### 1. Upgrade your local Pandoc version via Docker
First, upgrade your local version of Pandoc as specified in your Dockerfile and rebuild your image (i.e. `docker-compose build web`). [This PR should provide ample inspiration](https://github.com/scholastica/scholastica/pull/5502). Once upgraded, you can test the upgrade locally and make sure everything still works as expected. 

To be clear, this step has nothing to do with this buildpack – that comes in later steps.

#### 2. Create a new version of the Pandoc buildpack
Now that you're confident the new version works, you need to update this buildpack to point to the latest version of Pandoc. This is very easy and requires changing a few line in `bin/compile`. [This PR should provide ample inspiration](https://github.com/scholastica/pandoc-buildpack/pull/1).

Then, you need to merge your change into master and cut a new release. As described above, this can be done entirely via the Github web interface.

#### 3. Update Heroku cloud environments (i.e. staging, demo, production)
Then, you need to update all Heroku cloud environments to use your newly minted buildpack. This process looks like:

    # Remove existing buildpack (i.e. the old pandoc version)
    heroku buildpacks:remove https://github.com/scholastica/pandoc-buildpack.git#2.0.3 -a scholastica

    # Add new buildpack. Note: You'll need to update the tag number
    heroku buildpacks:add https://github.com/scholastica/pandoc-buildpack.git#2.3 -a scholastica

Note: You'll need to repeat these steps for all cloud environments (demo, staging, production).


