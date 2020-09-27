FROM ubuntu
RUN apt-get update
RUN apt-get install -y gnupg2 zsh git curl apt-transport-https && chsh -s $(which zsh)
RUN sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
RUN curl -fsSL https://github.com/rabbitmq/signing-keys/releases/download/2.0/rabbitmq-release-signing-key.asc | apt-key add -
RUN curl -fsSL https://github.com/rabbitmq/signing-keys/releases/download/2.0/rabbitmq-release-signing-key.asc | apt-key add -
RUN echo "deb https://dl.bintray.com/rabbitmq-erlang/debian focal erlang-23.x" > /etc/apt/sources.list.d/bintray.erlang.list
RUN echo "deb https://dl.bintray.com/rabbitmq/debian bionic main" > /etc/apt/sources.list.d/bintray.rabbit.list
RUN apt-get update -y
RUN apt-get install -y erlang-base \
                        erlang-asn1 erlang-crypto erlang-eldap erlang-ftp erlang-inets \
                        erlang-mnesia erlang-os-mon erlang-parsetools erlang-public-key \
                        erlang-runtime-tools erlang-snmp erlang-ssl \
                        erlang-syntax-tools erlang-tftp erlang-tools erlang-xmerl \
                        rabbitmq-server
RUN apt-get install -y gosu
COPY prebuildfs /
COPY rootfs /

ENV HOME="/root" \
    OS_ARCH="arm64" \
    OS_FLAVOUR="debian-10" \
    OS_NAME="linux"

ENV BITNAMI_APP_NAME="rabbitmq" \
    BITNAMI_IMAGE_VERSION="3.8.9-debian-10-r4" \
    LANG="en_US.UTF-8" \
    LANGUAGE="en_US:en"

EXPOSE 4369 5672 15672 25672

ENTRYPOINT [ "/opt/bitnami/scripts/rabbitmq/entrypoint.sh" ]
CMD [ "/opt/bitnami/scripts/rabbitmq/run.sh" ]

#FROM debian:buster-slim
#LABEL maintainer "Bitnami <containers@bitnami.com>"
#
#ENV HOME="/opt/bitnami/rabbitmq/.rabbitmq" \
#    OS_ARCH="amd64" \
#    OS_FLAVOUR="debian-10" \
#    OS_NAME="linux" \
#    PATH="/opt/bitnami/erlang/bin:/opt/bitnami/rabbitmq/sbin:/opt/bitnami/common/bin:$PATH"
#
#COPY prebuildfs /
## Install required system packages and dependencies
#RUN install_packages acl ca-certificates curl gzip libc6 libssl1.1 libtinfo6 locales procps tar zlib1g
#RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "erlang" "22.3.0-0" --checksum e9b6cba6a355dc2a6cc59829a59240d70cfb247f584a5f65f16fd6754c716166
#RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "rabbitmq" "3.8.9-0" --checksum e1cda0f8399694e9285482a04c212d8406bf610ee20b9144952a9d584ce8fd19
#RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "gosu" "1.12.0-1" --checksum 51cfb1b7fd7b05b8abd1df0278c698103a9b1a4964bdacd87ca1d5c01631d59c
#RUN apt-get update && apt-get upgrade -y && \
#    rm -r /var/lib/apt/lists /var/cache/apt/archives
#RUN chmod g+rwX /opt/bitnami
#RUN localedef -c -f UTF-8 -i en_US en_US.UTF-8
#RUN update-locale LANG=C.UTF-8 LC_MESSAGES=POSIX && \
#    DEBIAN_FRONTEND=noninteractive dpkg-reconfigure locales
#RUN echo 'en_GB.UTF-8 UTF-8' >> /etc/locale.gen && locale-gen
#RUN echo 'en_US.UTF-8 UTF-8' >> /etc/locale.gen && locale-gen
#
#COPY rootfs /
#RUN /opt/bitnami/scripts/rabbitmq/postunpack.sh
#RUN /opt/bitnami/scripts/locales/add-extra-locales.sh
#ENV BITNAMI_APP_NAME="rabbitmq" \
#    BITNAMI_IMAGE_VERSION="3.8.9-debian-10-r4" \
#    LANG="en_US.UTF-8" \
#    LANGUAGE="en_US:en"
#
#EXPOSE 4369 5672 15672 25672
#
#USER 1001
#ENTRYPOINT [ "/opt/bitnami/scripts/rabbitmq/entrypoint.sh" ]
#CMD [ "/opt/bitnami/scripts/rabbitmq/run.sh" ]
