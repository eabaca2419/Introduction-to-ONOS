# Mininet Installation
## Installing Mininet from Source
```
git clone https://github.com/mininet/mininet
```
## Installing the Latest Version
###### As of May 2022, the latest version of Mininet is 2.3.0.
> If you want to see what versions are available. Use the comand *git tag* after *cd mininet* to see the available versions.
```
cd mininet
git checkout -b mininet-2.3.0 2.3.0
cd ..
```
## Installing Mininet
```
mininet/util/install.sh 
```
## Running a simple Mininet Network test
```
sudo mn --switch ovsbr --test pingall
```
