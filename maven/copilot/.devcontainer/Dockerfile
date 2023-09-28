FROM maven:3-eclipse-temurin-17-alpine

ARG USER=dev-user
ARG USER_ID=1000
ARG DOCKER_GROUP=docker
ARG DOCKER_DEBIAN_GROUP_ID=994

RUN apk add --update \
  sudo \
  git \
  curl \
  openssh \
  docker \
  openrc

RUN curl -Lo copilot https://github.com/aws/copilot-cli/releases/latest/download/copilot-linux \
  && chmod +x copilot \
  && sudo mv copilot /usr/local/bin/copilot \
  && copilot --help

# add dev-user
RUN addgroup -S $USER \
  && adduser -S $USER -G $USER -u $USER_ID -s /bin/ash \
  && echo "$USER ALL=(ALL) NOPASSWD: ALL" >/etc/sudoers.d/$USER \
  && chmod 0440 /etc/sudoers.d/$USER \
  && addgroup $USER $DOCKER_GROUP \
  && addgroup -g $DOCKER_DEBIAN_GROUP_ID -S docker_debian \
  && addgroup $USER docker_debian
