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
## Installation 
###### ONOS Default Packages
> ONOS default packages assume ONOs gets installed under the directory /opt
```
sudo mkdir /opt
cd /opt
```
###### Downloading the desire ONOS Version
> The following lines are default using $ONOS_VERSION and can be replace with onos-2.7.0 since its the latest version.
```
sudo wget -c https://repo1.maven.org/maven2/org/onosproject/onos-releases/$ONOS_VERSION/onos-$ONOS_VERSION.tar.gz
sudo tar xzf onos-$ONOS_VERSION.tar.gz
sudo mv onos-$ONOS_VERSION onos
```
## Running ONOS
###### Running ONOS as a service
> Before running either the CLI or the GUI you need to start ONOS as a service.
```
sudo /opt/onos/bin/onos-service start
```
> If you receive an error shown below:
![Error](https://github.com/eabaca2419/Introduction-to-ONOS/blob/main/ONOS_Installation/Error_Running_ONOS_as_a_Service.png)
> Run the following comands and it should run correctly.
```
export CHECK_ROOT_INSTANCE_RUNNING=false
sudo /opt/onos/bin/onos-service stop
sudo /opt/onos/bin/onos-service start
```
###### Running the CLI
> Open another terminal while ONOS is running as a Service.
> When running the CLI there is several confligs if you use the follwoing line:
```
sudo /opt/onos/bin/onos
```
> It will ask for a password which can't be found anywhere. Instead run the following line:
```
ssh -p 8101 karaf@localhost
```
> Password: *karaf*
> 