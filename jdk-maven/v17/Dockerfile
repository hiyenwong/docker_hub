# openjdk version 11.0.16
# OpenJDK Runtime Environment 18.9
# OpenJDK 64-Bit Server VM 18.9

FROM ubuntu:jammy
MAINTAINER hiyenwong



ENV LANG='en_US.UTF-8' LANGUAGE='en_US:en' LC_ALL='en_US.UTF-8'
ARG ZULU_REPO_VER=1.0.0-3
ARG ZULU_REPO_SHA256=d08d9610c093b0954c6b278ecc628736e303634331641142fa5096396201f49c

# ensure local python is preferred over distribution python
ENV PATH /usr/local/bin:$PATH
ENV TZ Asia/Shanghai
RUN ln -fs /usr/share/zoneinfo/${TZ} /etc/localtime \
    && echo ${TZ} > /etc/timezone
# http://bugs.python.org/issue19846
# > At the moment, setting "LANG=C" on a Linux system *fundamentally breaks Python 3*, and that's not OK.



RUN apt-get -qq update && \
    apt-get -qq -y --no-install-recommends install gnupg software-properties-common locales curl tzdata wget && \
    echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && \
    locale-gen en_US.UTF-8 && \
    apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9 && \
    curl -sLO https://cdn.azul.com/zulu/bin/zulu-repo_${ZULU_REPO_VER}_all.deb && \
    echo "${ZULU_REPO_SHA256} zulu-repo_${ZULU_REPO_VER}_all.deb" | sha256sum --strict --check - && \
    dpkg -i zulu-repo_${ZULU_REPO_VER}_all.deb && \
    apt-get -qq update && \
    echo "Package: zulu17-*\nPin: version 17.0.8-*\nPin-Priority: 1001" > /etc/apt/preferences && \
    apt-get -qq -y --no-install-recommends install zulu17-jdk=17.0.8-* && \
    apt-get -qq -y purge --auto-remove gnupg software-properties-common curl && \
    rm -rf /var/lib/apt/lists/* zulu-repo_${ZULU_REPO_VER}_all.deb

ENV JAVA_HOME=/usr/lib/jvm/zulu17




# extra dependencies (over what buildpack-deps already includes)

#ADD sources.list /etc/apt/
ADD java.security /usr/local/openjdk-17/conf/security/

#RUN apt-get update
#RUN apt-get install --assume-yes apt-utils wget
#RUN
##RUN apt-get install -y build-essential
#RUN #apt-get install -y libsasl2-dev  libsasl2-modules libsasl2-dev
#RUN #apt-get install -y build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev

#RUN  apt-get install -y --no-install-recommends libbluetooth-dev tk-dev uuid-dev
#RUN rm -rf /var/lib/apt/lists/*
#RUN apt-get upgrade -y
# maven 3.9.3

RUN wget https://dlcdn.apache.org/maven/maven-3/3.9.3/binaries/apache-maven-3.9.3-bin.tar.gz
RUN tar xzvf apache-maven-3.9.3-bin.tar.gz
RUN cp -R apache-maven-3.9.3 /usr/local/bin
RUN export PATH=apache-maven-3.9.3/bin:$PATH
RUN export PATH=/usr/local/bin/apache-maven-3.9.3/bin:$PATH
RUN ln -s /usr/local/bin/apache-maven-3.9.3/bin/mvn /usr/local/bin/mvn


RUN wget https://downloads.apache.org/maven/mvnd/1.0-m7/maven-mvnd-1.0-m7-m40-linux-amd64.tar.gz
RUN tar xzvf maven-mvnd-1.0-m7-m40-linux-amd64.tar.gz
RUN cp -R /maven-mvnd-1.0-m7-m40-linux-amd64/bin/* /usr/local/bin


