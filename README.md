# Examples: Wordpress

My typical approach to Wordpress plugin and theme development, as a Dockerised Wordpress application.

## Quickstart

[Get Docker](https://www.docker.com/get-docker), then:

### 1. Clone this repo

```bash
git clone git@github.com:galbus/examples-wordpress.git
cd examples-wordpress
```

### 2. One-command setup

```bash
make install
```

wait a while...

### 3. Visit site

[http://localhost](http://localhost)

## Notes

### Plugin

`/wp-content/plugins/custom-plugin`

* The plugin follows an OO architecture which includes version numbers for both the plugin, and the database.
  * This enables us to write database upgrade scripts by comparing the version number in the plugin file to the version number stored in the database.
* Some example methods have been included, which:
  * adds a custom post type (Questions)
  * adds some custom user roles
  * removes some admin menu options

### Theme

`/wp-content/themes/custom-theme`
(this file will only exist after a successful `make install`)

* A [JointsWP](http://jointswp.com/) starter theme, ready for customisation.
  * JointsWP is a lot like [FoundationPress](https://foundationpress.olefredrik.com/), but with the added benefit that [Foundation for Sites](https://foundation.zurb.com/sites.html) can be updated much easier __(when I used FoundationPress I needed to wait for the project maintainer to update the Foundation for Sites package)__.
* This is a `git clone` of the JointsWP master branch.
* View the [JointsWP docs](http://jointswp.com/docs/) to see how to get started.

## Known issues

* Permissions on shared volumes need to be investigated as uploaded images and other assets aren't accessible by the web server
