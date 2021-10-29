# stepsforinstallations

ServerName      Public IP Address
Hackathon1        13.233.245.88  -  Asif
Hackathon2        13.233.130.108  - kishore
Hackathon3        35.154.25.173
Hackathon4        13.127.201.108
 
Linux Credentials:
 
Username: ninjaroot
Password: ninjaroot
 
Mysql Credentials:
 
Username: root
Password: H@ckath0n


PATH=$PATH:/usr/bin export PATH


ServerName      Public IP Addressw
Hackathon1        13.233.245.88  - asif
Hackathon2        13.233.130.108  - kishore
Hackathon3        35.154.25.173
Hackathon4        13.127.201.108
 
Linux Credentials:
 
Username: ninjaroot
Password: ninjaroot
 
Mysql Credentials:
 
Username: root
Password: H@ckath0n








   
dd if=/dev/zero of=/mnt/swapfile bs=1024 count=4097152
chmod 600 /mnt/swapfile
mkswap /mnt/swapfile
swapon /mnt/swapfile













                                               Mysql
                                            ------------
MySQL Database :
How to create a user and grant privileges.
[root@ip-172-31-24-48 opt]# mysql -u root -p
Enter password:
 
mysql> CREATE  USER 'inguser1'@'%' IDENTIFIED BY 'H@ckath0n';
Query OK, 0 rows affected (0.01 sec)      
 
mysql> GRANT ALL PRIVILEGES ON *.* to 'inguser1'@'%';
Query OK, 0 rows affected (0.00 sec)
 
mysql> flush privileges;
Query OK, 0 rows affected (0.00 sec)
 
mysql> exit
Bye
'[root@ip-172-31-24-48 opt]# mysql -u inguser1 -p
Enter password:
 
Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
 
mysql> create database ingdb;
Query OK, 1 row affected (0.00 sec)











                                            java installation
                                        ----------------------
cd /opt/
download java .
tar -xzvf jdk-8u261-linux-x64.tar.gz
cd jdk1.8.0_212/
alternatives --install /usr/bin/java java /opt/jdk1.8.0_291/bin/java 2
alternatives --config java
alternatives --install /usr/bin/jar jar /opt/jdk1.8.0_291/bin/jar 1
alternatives --install /usr/bin/javac javac /opt/jdk1.8.0_291/bin/javac 1
alternatives --set jar /opt/jdk1.8.0_291/bin/jar
alternatives --set javac /opt/jdk1.8.0_291/bin/javac

sudo vi /etc/environment

export JAVA_HOME=/opt/jdk1.8.0_302
export JRE_HOME=/opt/jdk1.8.0_302/jre
export PATH=$PATH:/opt/jdk1.8.0_302/bin:/opt/jdk1.8.0_302/jre/bin

:wq! -- to save and quit



                                                  jenkins installation
                                                 ----------------------
PATH=$PATH:/usr/bin export PATH
cd /opt
sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo
sudo rpm --import https://jenkins-ci.org/redhat/jenkins-ci.org.key
sudo yum install jenkins -y
systemctl start jenkins
chkconfig jenkins on
systemctl status jenkins then ctl+c to come back


To change default port go to : vi /etc/sysconfig/jenkins/
change the port and restart jenkins
 to open in UI give (IP:PORT NUMBER)

to instert in file give i
to save :wq!
to quit without saving :q!

To get the token
cat /var/lib/jenkins/secrets/initialAdminPassword


                                      MAVEN INSTALL
                                     ---------------
sudo wget http://mirrors.estointernet.in/apache/maven/maven-3/3.8.3/binaries/apache-maven-3.8.3-bin.tar.gz
tar -xvzf apache-maven-3.8.3-bin.tar.gz
cp -r apache-maven-3.8.3 maven




vi /etc/profile
export M2_HOME=/opt/maven
export PATH=${M2_HOME}/bin:${PATH}

source /etc/profile


 
                                                       Tomcat installation
                                                      ---------------------
PATH=$PATH:/usr/bin export PATH
sudo wget http://mirrors.estointernet.in/apache/tomcat/tomcat-9/v9.0.54/bin/apache-tomcat-9.0.54.tar.gz
https://mirror.olnevhost.net/pub/apache/tomcat/tomcat-9/v9.0.54/bin/apache-tomcat-9.0.54.tar.gz
sudo tar -xvzf apache-tomcat-9.0.54.tar.gz 


vim /opt/apache-tomcat-9.0.53/webapps/manager/META-INF/context.xml and follow same steps for hostmanager/MET-INF/context.xml also.
 
 <Context antiResourceLocking="false" privileged="true" >
 <!--  <Valve className="org.apache.catalina.valves.RemoteAddrValve"
  allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" />
 -->
  <Manager sessionAttributeValueClassNameFilter="java\.lang\.(?:Boolean|Integer|Long|Number|String)|org\.apache\.catalina\.filters\.CsrfPreventionFilter\$LruCache(?	:\$1)?|java\.util\.(?:Linked)?HashMap"/>
 </Context>


To configure Tomcat credentials

vim /opt/apache-tomcat-9.0.50/conf/tomcat-users.xml
 
line no 37
<role rolename="manager-script"/>
<role rolename="manager-gui"/>
<user username="tomcat" password="tomcat" roles="manager-script,manager-gui"/>

alternate

vi /opt/apache-tomcat-9.0.17/webapps/host-manager/META-INF/context.xml
<!-- <value.......--> -->
vi /opt/apache-tomcat-9.0.17/webapps/manager/META-INF/context.xml
<!-- <value.......--> -->
ll
cd conf/
ll
vi tomcat-users.xml
<user username="admin" password="admin" roles="manager-gui,admin-gui,manager-script"/>

71 cd ..
72 cd bin/
73 sh shutdown.sh
74 sh startup.sh
75 sh shutdown.sh
76 cd







<user username="admin" password="admin" roles="manager-gui,admin-gui,manager-script"/>

port-8090
user -admin
pwd-admin


                                              Nexus installation: will install in root only.start in root only
                                              --------------------

new - sudo wget http://www.sonatype.org/downloads/nexus-latest-bundle.zip
sudo chmod 777 nexus-latest-bundle.zip
sudo unzip nexus-latest-bundle.zip
cd  nexus-2.14.13-01/bin
PATH=$PATH:/usr/bin export PATH
RUN_AS_USER=root ./nexus start

8081--default port   - publicip:8081/nexus
default credentials are:
admin
admin123




issue :

not able to upload in nexus

goto settings.xml  /opt/maven/conf/settings.xml and change the properties
--------------------------------
/opt/maven/conf<server>
      <server>
      <id>nexus</id>
      <username>admin</username>
      <password>admin123</password>
    </server>




                                         Sonarqube Installation  - ninjaroot
                                     ===============================================

cd /opt
sudo wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-8.9.2.zip
https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-8.6.0.39681.zip
sudo unzip sonarqube-9.1.zip
we need to give full permission to sonarqube.7.6. (we need to run as ec2-user)
sudo chown -R ec2-user:ec2-user /opt/sonarqube-7.6
sudo chmod 777 -R sonarqube7.6
cd sonarqube-7.6/bin/linux-x86-64


ls
sh sonar.sh start
sh sonar.sh status

publicip:9000

UN:admin
PW:admin

wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-3.3.0.1492-linux.zip
https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.6.0.2311-linux.zip
unzip sonar-scanner-cli-3.3.0.1492-linux.zip
cd sonar-scanner-cli-3.3.0.1492-linuxd 
vim /etc/environment

check and add
export SONAR_SCANNER=/opt/sonar-scanner-4.6.0.2311-linux
export PATH=${SONAR_SCANNER}/bin:${PATH}


--we nee to add sonar in global tool configuraion.
check withere sonar running or not.





Node-JS:
=============================================
https://nodejs.org/dist/v10.15.3/node-v10.15.3-linux-x64.tar.xz
tar -zxvf node-v10.15.3-linux-x64.tar.xz


set the class path
export NODE_HOME=/opt/node-v10.15.3-linux-x64
export PATH=${NODE_HOME}/bin:${PATH}

alternatives

NODEJS & NPM
=====================================================================================
yum install -y gcc-c++ make
curl -sL https://rpm.nodesource.com/setup_10.x | sudo -E bash -
yum install nodejs -y
npm install yarn -g


vim /etc/environment
export NODE_HOME=/usr/bin/node
export PATH=${NODE_HOME}/bin:${PATH}

node --version
npm -version
POLYMER
npm install -g polymer-cli --unsafe-perm


=====================================================================================
POLYMER


Mariadb10 installation
vi /etc/yum.repos.d/MariaDB.repo
udo
[mariadb]
name = MariaDB
baseurl = http://yum.mariadb.org/10.1/rhel7-amd64
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
gpgcheck=1
yum install MariaDB-server MariaDB-client -y

systemctl start mariadb
systemctl enable mariadb
systemctl status mariadb






                                                                  CI/CD
                                                                ---------

download plugins -  

maven integration 
jacoco
sonar scanner



-------------------

add java and maven git in global tool configuraiton.



issue :

not able to upload in nexus

goto settings.xml  we need to add /opt/maven/conf/settings.xml and change the properties
--------------------------------
/opt/maven/conf<server>

      <id>nexus</id>
      <username>admin</username>
      <password>admin123</password>
    </server>


nexus repository create new repository
add - hosted 















   


