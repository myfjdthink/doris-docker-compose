FROM apache/incubator-doris:build-env-ldb-toolchain-latest

WORKDIR /opt/

#RUN wget https://dist.apache.org/repos/dist/release/doris/1.0/1.0.0-incubating/apache-doris-1.0.0-incubating-bin.tar.gz &&\
#  tar -zxvf apache-doris-1.0.0-incubating-bin.tar.gz &&\
#  mv apache-doris-1.0.0-incubating-bin doris

COPY ../apache-doris-1.0.0-incubating-bin.tar.gz .
RUN tar -zxvf apache-doris-1.0.0-incubating-bin.tar.gz &&\
    mv apache-doris-1.0.0-incubating-bin doris

ENTRYPOINT ["sh", "-c", "DORIS_HOME=/opt/doris/be/ PATH=$PATH:$DORIS_HOME/bin start_be.sh"]