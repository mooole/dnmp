FROM mysql:5.7

# ARGS
ARG CHANGE_SOURCE=false

# Change Timezone
ARG TIME_ZONE=UTC
RUN ln -snf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo "Asia/Shanghai" > /etc/timezone

# Change China Sources
COPY sources.list /etc/apt/sources.list

RUN apt-get -y update

# Install Base Components
RUN apt-get install -y --no-install-recommends cron vim curl

