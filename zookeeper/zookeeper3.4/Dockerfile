FROM tg10020607/base:v1.0

MAINTAINER tg10020607

ENV ZOOKEEPER_VERSION 3.4.14

# 下载zookeeper
RUN wget http://mirror.vorboss.net/apache/zookeeper/zookeeper-${ZOOKEEPER_VERSION}/zookeeper-${ZOOKEEPER_VERSION}.tar.gz && \
wget https://www.apache.org/dist/zookeeper/KEYS && \
wget https://www.apache.org/dist/zookeeper/zookeeper-${ZOOKEEPER_VERSION}/zookeeper-${ZOOKEEPER_VERSION}.tar.gz.asc && \
#wget -q https://www.apache.org/dist/zookeeper/zookeeper-${ZOOKEEPER_VERSION}/zookeeper-${ZOOKEEPER_VERSION}.tar.gz.md5

# 验证
# RUN md5sum -c zookeeper-${ZOOKEEPER_VERSION}.tar.gz.md5 && \
# gpg --import KEYS && \
# gpg --verify zookeeper-${ZOOKEEPER_VERSION}.tar.gz.asc

gpg --import KEYS && \
#gpg --verify zookeeper-${ZOOKEEPER_VERSION}.tar.gz.asc zookeeper-${ZOOKEEPER_VERSION}
gpg --verify zookeeper-${ZOOKEEPER_VERSION}.tar.gz.asc

# 安装
RUN tar -xzf zookeeper-${ZOOKEEPER_VERSION}.tar.gz -C /opt

# 配置
RUN mv /opt/zookeeper-${ZOOKEEPER_VERSION}/conf/zoo_sample.cfg /opt/zookeeper-${ZOOKEEPER_VERSION}/conf/zoo.cfg

ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64
ENV ZK_HOME /opt/zookeeper-${ZOOKEEPER_VERSION}
ENV ZK_HOME /opt/zookeeper-${ZOOKEEPER_VERSION}

ADD start-zk.sh /usr/bin/start-zk.sh 
EXPOSE 2181 2888 3888

WORKDIR /opt/zookeeper-${ZOOKEEPER_VERSION}
VOLUME ["/opt/zookeeper-${ZOOKEEPER_VERSION}/conf", "/opt/zookeeper-${ZOOKEEPER_VERSION}/data"]

CMD /usr/sbin/sshd && bash /usr/bin/start-zk.sh
