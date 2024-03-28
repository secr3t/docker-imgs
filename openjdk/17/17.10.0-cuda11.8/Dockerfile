FROM nvidia/cuda:11.8.0-cudnn8-runtime-rockylinux8

# Install Packages
RUN dnf -y update && \
    dnf -y install wget && \
    dnf -y install glibc-locale-source glibc-langpack-en && \
    dnf clean all

# 언어 설정
RUN localedef -f UTF-8 -i ko_KR ko_KR.UTF-8
ENV LC_ALL ko_KR.UTF-8
ENV LANGUAGE ko_KR.UTF-8

# 타임존 설정
ENV TZ=Asia/Seoul
RUN ln -snf /usr/share/zoneinfo/${TZ} /etc/localtime && \
    echo ${TZ} > /etc/timezone

ENV JAVA_VERSION 17.0.10.8.1
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

#ENV ARCH="x86_64"
#ENV DISTRO="rhel8"
#ENV REPO_URL https://developer.download.nvidia.com/compute/cuda/repos/${DISTRO}/${ARCH}/cuda-${DISTRO}.repo
#RUN dnf config-manager --add-repo ${REPO_URL}

RUN dnf install dnf-plugins-core -y

RUN mkdir tmp-content && \
    dnf download libcublas-12-0 && \
    rpm2cpio libcublas-12-0* | cpio -idmv --directory=tmp-content

RUN mv /tmp-content/usr/local/cuda-12.0/targets/*-linux/lib/* /usr/local/cuda/lib64/ && \
    rm -rf /tmp-content