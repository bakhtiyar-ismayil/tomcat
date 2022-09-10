# Apache Tomcat 

Tomcat is an open source Java implementation package developed by the Apache Software Foundation. I will show how to install Tomcat 9 on CentOS 7 in this tutorial.Tomcat 9 requires Java SE 8 or later. For this reason we will install OpenJDK, the open-source implementation of the Java Platform ,which is the default Java development and runtime in CentOS 7. Open your shell and create a java directory. 

**# mkdir -p /usr/share/java && cd /usr/share/java**

**# wget https://download.java.net/java/GA/jdk19/877d6127e982470ba2a7faa31cc93d04/36/GPL/openjdk-19_linux-x64_bin.tar.gz**

**# tar -xvf j***

**~ vim ~/.bashrc**

PATH=$PATH:$JAVA_HOME/bin
JAVA_HOME=/usr/share/java 

![img](/apache/tomcat/img/tomcat1.png)

**~ source ~/.bashrc**

![img](/apache/tomcat/img/tomcat2.png)
 
Running Tomcat as the root user is a security risk and not considered best practice. We’ll create a new system user for that and will specify tomcat username. You can specify what wolud you like. 

**# useradd tomcat01 && passwd tomcat01**

Create Directory  for all tomcat files  and preapre user for tomcat (TOMCAT_BASE). (Don't forget to use "/",add this user to sudoers file.).

**# mkdir /tomcat && ll /**

**# chown tomcat01:tomcat01 -R /tomcat**

**# cd /tomcat && wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.65/bin/apache-tomcat-9.0.65.tar.gz**

**# tar -xvf a***

 We can run ./startup.sh and tomcat will start, and may test this. 

**# sudo netstat -tulpan | grep LISTEN**

![img](/apache/tomcat/img/tomcat3.png)

This method only for "single instance" , but we will create "multi instance". 

**# mkdir instances**
 
**# cp apache-tomcat-9.0.65/ instances/instance1 -pr** 

![img](/apache/tomcat/img/tomcat4.png)

Now we can open **# cd /tomcat/instances/instance/bin** and run **#./startup.sh** or can create a script which will start our tomcat

**# mkdir controller**

**# vim start.sh**

#!/bin/bash

instance_name=$1

TOMCAT_BASE=/tomcat

INSTANCE_BASE=$TOMCAT_BASE/instances

CATALINA_HOME=$TOMCAT_BASE/apache-tomcat-9.0.65

CATALINA_BASE=$INSTANCE_BASE/$instance

export CATALINA_BASE CATALINA_HOME

$CATALINA_HOME/bin/startup.sh

**# chmod +x start.sh**

./start.sh instance1

![img](/apache/tomcat/img/tomcat5.png)


![img](/apache/tomcat/img/tomcat6.png)


![img](/apache/tomcat/img/tomcat7.png)




