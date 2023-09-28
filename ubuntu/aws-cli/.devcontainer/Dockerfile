FROM ubuntu:22.04

ARG USER=dev-user
ARG USER_ID=1000

RUN apt-get update \
    && apt-get install -y \
    sudo \
    git \
    curl \
    less \
    groff \
    glibc-tools \
    unzip


# add dev-user
RUN groupadd --gid $USER_ID $USER \
    && useradd --uid $USER_ID --gid $USER_ID --shell /bin/bash --create-home $USER \
    && echo $USER ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USER \
    && chmod 0440 /etc/sudoers.d/$USER

RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" \
    && unzip awscliv2.zip \
    && sudo ./aws/install