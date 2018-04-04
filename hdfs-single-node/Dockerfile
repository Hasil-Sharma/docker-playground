FROM ubuntu:14.04
WORKDIR /home
EXPOSE 50070
# ADD hadoop-2.9.0.tar.gz /home
RUN apt-get update && \
 apt-get upgrade -y && \
 apt-get install -y ssh vim rsync aria2 openjdk-7-jdk && \
 aria2c -x 10 "http://apache.claz.org/hadoop/common/stable/hadoop-2.9.0.tar.gz" && \
 tar -xf hadoop-2.9.0.tar.gz && \
 rm -rf hadoop-2.9.0.tar.gz && \
 echo "set nu" >> ~/.vimrc && \
 echo "export JAVA_HOME=$(readlink -f "$(which java)" | sed -e "s/bin\/java//")" >> ~/.bashrc && \
 sed -i "\$i <property><name>fs.defaultFS</name><value>hdfs://localhost:9000</value></property>" hadoop-2.9.0/etc/hadoop/core-site.xml && \
 sed -i "\$i <property><name>dfs.replication</name><value>1</value></property>" hadoop-2.9.0/etc/hadoop/hdfs-site.xml && \
 ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa && \
 cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys && \
 chmod 0600 ~/.ssh/authorized_keys && \
 echo "Host *" >> ~/.ssh/config && \
 echo "\tStrictHostKeyChecking no" >> ~/.ssh/config && \
 service ssh restart && \
 echo "export JAVA_HOME=$(readlink -f "$(which java)" | sed -e "s/bin\/java//")" >>  hadoop-2.9.0/etc/hadoop/hadoop-env.sh
WORKDIR /home/hadoop-2.9.0
RUN bin/hdfs namenode -format && \
  service ssh restart && \
  sbin/start-dfs.sh && \
  echo 'export PATH=$PATH:/home/hadoop-2.9.0/bin' >> ~/.bashrc && \
  bin/hdfs dfs -mkdir /user && \
  bin/hdfs dfs -mkdir /user/root
ENTRYPOINT service ssh restart && /home/hadoop-2.9.0/sbin/start-dfs.sh && /bin/bash
WORKDIR /home
