# hadoop配置

配置完成后下载必要的工具

```shell
sudo yum install net-tools
sudo yum install vim
```

创建文件夹soft存入两个资源安装包

hadoop-2.7.1.tar.gz

jdk-8u381-linux.rpm

安装

```shell
sudo rpm -ivh jdk-...rpm
sudo tar -zxvf ...tar.gz
```

关闭防火墙

```shell
sudo systemctl stop firewalld.service
sudo systemctl disable firewalld.service
```

关闭selinux

```shell
sudo vim /etc/selinux/config
enforcing->disabled
```

添加hadoop环境

```shell
sudo vim /etc/profile.d/hdfs.sh
export HADOOP_HOME=/opt/hadoop-2.7.1
export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin
```

创建HDFS的NN和DN目录

```shell
sudo mkdir /var/big_data
```

为Hadoop提供JAVA解释器路径信息

```shell
 vim hadoop-env.sh
export JAVA_HOME=/usr/java/default
```

为Yarn任务、资源管理器提供Java运行环境

```shell
vim yarn-env.sh
export JAVA_HOME=/usr/java/default
```

配置HDFS主节点信息、持久化和数据文件的主目录

```shell
vim core-site.xml
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://node01:9000</value>
    </property>
    <property>
        <name>hadoop.tmp.dir</name>
        <value>/var/big_data</value>
    </property>
```

配置HDFS默认的数据存放策略

```shell
vim hdfs-site.xml
    <property>
        <name>dfs.replication</name>
        <value>2</value>
    </property>
    <property>
        <name>dfs.namenode.secondary.http-address</name>
        <value>node03:50090</value>
    </property>
```

配置mapreduce任务调度策略

```shell
vim mapred-site.xml	
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
```

配置Yarn资源管理角色的信息

```shell
vim yarn-site.xml
    <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>
    <property>
        <name>yarn.resourcemanager.hostname</name>
        <value>node01</value>
    </property>
```

配置datanode节点信息

```shell
vim slaves
    node01
	node02
    node03
```

提前准备主机名解析文件
注意屏蔽或删除上面的127.0.0.1的信息

```shell
sudo vim /etc/hosts
        192.168.56.80  node01
        192.168.56.81  node02
        192.168.56.82  node03
```

克隆后，修改node02、node03的IP和主机名

```shell
sudo vim /etc/sysconfig/networ-scripts/ifcfg-ens33
sudo vim /etc/hostname
```

下面开始配置集群的ssh免密

```shell
ssh-keygen -t rsa
ssh-copy-id node01
ssh-copy-id node02
ssh-copy-id node03
```

格式化hdfs

```shell
hdfs namenode -format
```

