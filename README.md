# Hadoop1_script_singlenode
#Single Node Installation
sudo apt-get update
ssh-keygen
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
----**downloading and installing java (Hadoop requires a working Java 1.6+)**----
sudo apt-get install openjdk-8-jdk -y
-----------------------------**downloading hadoop**------------------------
wget
https://archive.apache.org/dist/hadoop/common/hadoop-1.2.1/hadoop-1.2.1.tar.gz
tar -xzvf hadoop-1.2.1.tar.gz
sudo mv hadoop-1.2.1 /usr/local/hadoop
---------------------------**configuring bashrc linux env setup**---------------
#Configuring bashrc linux env setup
nano ~/.bashrc
export HADOOP_PREFIX=/usr/local/hadoop/
export PATH=$PATH:$HADOOP_PREFIX/bin
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
export PATH=$PATH:$JAVA_HOME
#Setting hadoop env
nano /usr/local/hadoop/conf/hadoop-env.sh
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
export HADOOP_OPTS=-Djava.net.preferIPV4Stack=true
#Configuring core-site.xml
nano /usr/local/hadoop/conf/core-site.xml
<property>
<name>fs.default.name</name>
<value>hdfs://localhost:9000</value>
</property>
<property>
<name>hadoop.tmp.dir</name>
<value>/usr/local/hadoop/tmp</value>
</property>
#Configuring hdfs-site.xml
nano /usr/local/hadoop/conf/hdfs-site.xml
<property>
<name>dfs.replication</name>
<value>1</value>
</property>
#Configuring mapred-site.xml
nano /usr/local/hadoop/conf/mapred-site.xml
<property>
<name>mapred.job.tracker</name>
<value>hdfs://localhost:9001</value>
</property>
----------**making tmp dir**---------
mkdir /usr/local/hadoop/tmp
-------------**exec bash**-------
exec bash
----------------**formatting hadoop namenode**--------------
hadoop namenode -format
---------------**starting hadoop services(daemons)**-------------------
start-dfs.sh
Start-mapred.sh
jps
