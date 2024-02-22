(可选) 1修改/etc/hosts中的配置 
配置主机名映射 
10.254.3.75 VM1
10.254.2.226 VM2
10.254.2.253 VM3
(可选)2 配置ssh免密登录 方便机器之间远程登录
ssh-keygen -t rsa -b 4096 
ssh-copy-id VM1
ssh-copy-id VM2
ssh-copy-id VM3

3创建使用hadoop的用户 并配置ssh免密登录

部署hdfs集群：
在VM1上安装hadoop并执行下面操作

4配置hadoop-env.sh
加入一些路径

5修改原core-sie.xml 
主要加这一段： （如果配置主机名映射需使用ip）
  <property>
    <name>fs.defaultFS</name>
    <value>hdfs://VM1:8020</value>
  </property>
配置通信端口,主机为namenode启动的那台机器

6修改workers文件 
想让那些机器启动datanode,写那些机器 如VM2 VM3

7修改hdfs-site.xml 指定元数据存储位置，一些设置等等。 等会需要手动创建指定的文件夹，或指定存在的文件夹。不然会启动失败

8在相关路径准备上一步指定的文件目录

将hadoop分发到VM2 VM3 使用scp

9在3台机器的linux系统中加入hadoop环境变量

10 确保以上的全部文件所属用户为hadoop

11以hadoop用户格式化namenode然后启动hdfs集群


部署yarn集群
在VM1中
1 在mapred-env.sh中加入环境变量
2配置mapred-site.xml
3在yarn-site.xml中加入环境变量
4配置yarn.site.xml

将修改的文件分发到其它机器

启动yarn集群










