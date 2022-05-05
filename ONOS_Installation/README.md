# Installation of ONOS
## Requirements before installing ONOS
###### USERS
> ONOS shouldn't run as a root since it is a production service. Scripts used by ONOS need to run as a service requires a unprivilaged user. This often written as 'sdn'.
```
sudo adduser sdn --system --group
```
###### Software Packages
> ONOS is Java based platfrom. The follworing commands are used to are used to install Oracle Java 1.8.
```
sudo apt install openjdk-11-jdk
sudo nano /etc/enviroment
    add "JAVA_HOME=/usr/lib/jvm/java-1-openjdk-amd64"
```
> Install *Curl* sicne it will be used later on.
```
sudo apt-get install curl
```