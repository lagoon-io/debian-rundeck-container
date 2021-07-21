FROM nginx:1.19

ARG COMMON_PACKAGES="vim apt-transport-https ca-certificates wget dirmngr gnupg software-properties-common"

COPY ./conf/nginx/conf.d/server.conf /etc/nginx/conf.d/server.conf
COPY ./conf/nginx/ssl/server.crt /etc/nginx/conf.d/server.crt
COPY ./conf/nginx/ssl/server.key /etc/nginx/conf.d/server.key

# 基本設定
RUN apt update -y && \
  apt install -y $COMMON_PACKAGES && \
  chmod 644 /etc/nginx/conf.d/server.crt && \
  chmod 644 /etc/nginx/conf.d/server.key

# RUN wget -qO - https://adoptopenjdk.jfrog.io/adoptopenjdk/api/gpg/key/public | apt-key add - 
# RUN     add-apt-repository --yes https://adoptopenjdk.jfrog.io/adoptopenjdk/deb/ 
# RUN     apt update -y 
# # Oracle Javaと互換性のあるHotSpot版をインストールできなかったので、OpenJ9版を採用
# RUN apt install -y adoptopenjdk-8-openj9
# # RUN     apt install -y adoptopenjdk-8-hotspot

RUN cd ~/ && \
    wget https://github.com/AdoptOpenJDK/openjdk8-binaries/releases/download/jdk8u292-b10/OpenJDK8U-jre_x64_linux_hotspot_8u292b10.tar.gz && \
    tar xzf OpenJDK8U-jre_x64_linux_hotspot_8u292b10.tar.gz && \
    export PATH=$PWD/jdk8u292-b10-jre/bin:$PATH && \
    echo "export PATH=$PWD/jdk8u292-b10-jre/bin:$PATH" >> ~/.bashrc

RUN  cd /tmp && \
  wget https://download.rundeck.org/deb/rundeck-2.6.11-1-GA.deb && \
  dpkg -i rundeck-2.6.11-1-GA.deb && \
  service rundeck enable
