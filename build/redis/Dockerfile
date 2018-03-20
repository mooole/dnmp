FROM redis:4.0.8

# Change Timezone
ARG TIME_ZONE=UTC
RUN ln -snf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo "Asia/Shanghai" > /etc/timezone

CMD [ "redis-server", "/usr/local/etc/redis/redis.conf" ]