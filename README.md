# Examples: Wordpress

A quick example of my typical overall approach to Wordpress plugin and theme development.

As this is a demo of both plugin __and__ theme development, the entire project is a Dockerised Wordpress application. 

If I were only working on individual plugins or themes then the project wouldn't include all the Docker stuff, and the plugin/theme would ideally be published to a private repo for simpler install and updates.

## Quickstart

[Get Docker](https://www.docker.com/get-docker), then:

### Clone repo

```bash
git clone git@github.com:galbus/examples-wordpress.git
cd examples-wordpress
```

### Docker up

```bash
docker-compose up -d
alias wp="docker-compose run --rm my-wpcli"
wp --info # This should output some WP-CLI info
```

### Install Composer packages

Install [Composer](https://getcomposer.org/) (globally, using e.g. `mv composer.phar /usr/local/bin/composer`)

```bash
composer install
```

In this example, this installs any composer packages required by the `pressingspace-example` plugin.

### Install Wordpress

```bash
cd public/
wp core download
wp core install --url="localhost" --title="Pressing Space: Wordpress Examples" --admin_user="admin" --admin_password="password" --admin_email="stuart.mcalpine@pressingspace.com"
wp rewrite structure '/%postname%/'
```

### Install example Wordpress plugin

```bash
wp plugin activate pressingspace-example
```

### Install example Wordpress theme

```bash
wp theme activate pressingspace-example
```

### Install other Wordpress plugins (optional)

```bash
wp plugin install post-thumbnail-editor --activate
```

### Build theme

[Install npm](https://www.npmjs.com/), then:

```bash
cd wp-content/themes/pressingspace-example/
npm install
```

### Visit site

[http://localhost:8080](http://localhost:8080)

## Notes

### Example Plugin

`/public/wp-content/plugins/pressingspace-example`

* The plugin follows an OO architecture which includes version numbers for both the plugin and the database.
    * This enables us to write database upgrade scripts by comparing the version number in the plugin file to the version number stored in the database.
* As this example has been prepared overnight there is limited functionality. I've provided some example methods which add custom post types and remove options from the admin menu.
* I would have liked to demonstrate some 3rd-party API integration, but time hasn't allowed this.

### Example Theme

`/public/wp-content/themes/pressingspace-example`

* I've recently been using [JointsWP](http://jointswp.com/) as a start for theme development.
* JointsWP is a lot like [FoundationPress](https://foundationpress.olefredrik.com/), but the [Foundation for Sites](https://foundation.zurb.com/sites.html) npm package can be updated a lot easier __(I found with JointsWP that you had to wait until the project maintainer had upgraded Foundation, which isn't ideal)__.
* As this example has been prepared overnight the styling and base functionality has been left untouched. The next step would be to apply styles and write any custom (__theme-specific__) PHP/JavaScript for the theme.
