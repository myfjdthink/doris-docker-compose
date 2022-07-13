FROM apache/incubator-doris:build-env-ldb-toolchain-latest

WORKDIR /opt/

#RUN wget https://dist.apache.org/repos/dist/release/doris/1.0/1.0.0-incubating/apache-doris-1.0.0-incubating-bin.tar.gz &&\
#  tar -zxvf apache-doris-1.0.0-incubating-bin.tar.gz &&\
#  mv apache-doris-1.0.0-incubating-bin doris

# for local debug
COPY ../apache-doris-1.0.0-incubating-bin.tar.gz .
RUN tar -zxvf apache-doris-1.0.0-incubating-bin.tar.gz &&\
    mv apache-doris-1.0.0-incubating-bin doris

RUN alternatives --set java java-1.8.0-openjdk.x86_64 &&\
    alternatives --set javac java-1.8.0-openjdk.x86_64 &&\
    export JAVA_HOME=/usr/lib/jvm/java-1.8.0

# RUN yum install net-tools -y

# config fe priority_networks
EXPOSE 8030 9083

ENTRYPOINT ["sh", "-c", "DORIS_HOME=/opt/doris/fe/ PATH=$PATH:$DORIS_HOME/bin start_fe.sh"]