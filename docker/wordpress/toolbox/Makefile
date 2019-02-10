WP_CLI=wp-cli --allow-root

install: download configure

download:
	@echo "⬇️  Downloading Wordpress..."

	$(WP_CLI) core download \
		--version=${WORDPRESS_VERSION} \
		--locale=${WORDPRESS_LOCALE} \

configure:
	@echo "⚙️  Configuring Wordpress database..."
	@rm -f wp-config.php
	$(WP_CLI) core config \
		--dbhost=${WORDPRESS_DB_HOST} \
		--dbname=${WORDPRESS_DB_NAME} \
		--dbuser=${WORDPRESS_DB_USER} \
		--dbpass=${WORDPRESS_DB_PASSWORD} \
		--locale=${WORDPRESS_LOCALE} \
		--skip-check

	@echo "⚙️  Configuring Wordpress parameters..."
	$(WP_CLI) core install \
		--url=${WORDPRESS_WEBSITE_URL_WITHOUT_HTTP} \
		--title="$(WORDPRESS_WEBSITE_TITLE)" \
		--admin_user=${WORDPRESS_ADMIN_USER} \
		--admin_password=${WORDPRESS_ADMIN_PASSWORD} \
		--admin_email=${WORDPRESS_ADMIN_EMAIL}

	$(WP_CLI) option update siteurl "${WORDPRESS_WEBSITE_URL}"
	$(WP_CLI) rewrite structure $(WORDPRESS_WEBSITE_POST_URL_STRUCTURE)

	@echo "⚙️  Updating wp-config.php"
	$(WP_CLI) config set WP_DEBUG ${WORDPRESS_DEBUG} --raw
	$(WP_CLI) config set WP_HOME ${WORDPRESS_WEBSITE_URL}
	$(WP_CLI) config set WP_SITEURL ${WORDPRESS_WEBSITE_URL}
	$(WP_CLI) config set WP_CONTENT_DIR ${WORDPRESS_CONTENT_DIRECTORY}
	$(WP_CLI) config set WP_CONTENT_URL ${WORDPRESS_WEBSITE_URL}/wp-content

	@echo "⚙️  Activating Starter Plugin"
	$(WP_CLI) plugin activate ${WORDPRESS_PLUGIN_ID}

	@echo "⬇️  Downloading JointsWP Starter Theme"
	git clone --depth=1 https://github.com/JeremyEnglert/JointsWP.git ${WORDPRESS_CONTENT_DIRECTORY}/themes/${WORDPRESS_THEME_ID}
	rm -rf ${WORDPRESS_CONTENT_DIRECTORY}/themes/${WORDPRESS_THEME_ID}/.git

	@echo "⚙️  Activating JointsWP Starter Theme"
	$(WP_CLI) theme activate ${WORDPRESS_THEME_ID}
