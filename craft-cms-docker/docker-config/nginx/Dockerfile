FROM nginx:1.15

# Copy our project's default nginx configuration file
COPY ./docker-config/nginx/default.conf /etc/nginx/conf.d/default.conf

# Copy our Craft CMS project's web folder into the nginx static files folder
COPY --chown=www-data:www-data ./src/web /var/www/html/web