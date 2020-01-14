FROM nginx:1.16.1

# Change Timezone
ARG TIME_ZONE=UTC
RUN ln -snf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo "Asia/Shanghai" > /etc/timezone

# Change Webroot Permissions
RUN mkdir -p /var/www/html
RUN groupadd -r www && useradd -r -g www www
RUN chown -R www.www /var/www/html /var/log/nginx

WORKDIR /var/www/html