FROM rockylinux/rockylinux:9

MAINTAINER secr3t <dev.secr3@gmail.com>

# Install Packages
RUN yum update -y && \
    yum install -y wget && \
    yum -y install glibc-locale-source glibc-langpack-en && \
    yum clean all

# 언어 설정
RUN localedef -f UTF-8 -i ko_KR ko_KR.UTF-8
ENV LC_ALL ko_KR.UTF-8
ENV LANGUAGE ko_KR.UTF-8

# 타임존 설정
ENV TZ=Asia/Seoul
RUN ln -snf /usr/share/zoneinfo/${TZ} /etc/localtime && \
    echo ${TZ} > /etc/timezone

ENV JAVA_VERSION 17.0.9.8.1
ENV JAVA_DIR jdk-${JAVA_VERSION}
ENV JAVA_FILE jdk-${JAVA_VERSION}.tar.gz
ENV JAVA_HOME /usr/local/${JAVA_DIR}


ENV DOWNLOAD_URL https://corretto.aws/downloads/resources/${JAVA_VERSION}/amazon-corretto-${JAVA_VERSION}-linux-x64.tar.gz
ENV UNARCHIVE_DIR_NAME amazon-corretto-${JAVA_VERSION}-linux-x64

# JAVA 설치
RUN cd /usr/local/src && \
    wget ${DOWNLOAD_URL} -O ${JAVA_FILE} && \
    tar xzf ${JAVA_FILE} && \
    mv ${UNARCHIVE_DIR_NAME} ${JAVA_DIR} && \
    rm -f ${JAVA_FILE} && \
    mv ${JAVA_DIR} ${JAVA_HOME}

# JAVA_HOME PATH 등록
ENV PATH="$PATH:$JAVA_HOME/bin"
