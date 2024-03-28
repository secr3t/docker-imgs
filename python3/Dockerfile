FROM nvidia/cuda:12.1.0-cudnn8-runtime-rockylinux8 as base

# Install Packages
RUN dnf -y update && \
    dnf -y install wget && \
    dnf -y install glibc-locale-source glibc-langpack-en

FROM base
RUN dnf -y install python3.9 && \
    dnf clean all

# 언어 설정
RUN localedef -f UTF-8 -i ko_KR ko_KR.UTF-8
ENV LC_ALL ko_KR.UTF-8
ENV LANGUAGE ko_KR.UTF-8

# 타임존 설정
ENV TZ=Asia/Seoul
RUN ln -snf /usr/share/zoneinfo/${TZ} /etc/localtime && \
    echo ${TZ} > /etc/timezone

RUN pip3 install paddlepaddle paddleocr flask
RUN python3 -m pip install paddlepaddle-gpu==2.6.1