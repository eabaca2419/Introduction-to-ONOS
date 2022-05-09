# P4Runtime Basics
## System Requirements
###### Docker v1.13.0+
###### make
###### Python 3
###### Bash-like Unix shell
> Install Docker
```
sudo apt install docker compose
```
> Install make
```
sudo apt install make
```
## New Generation SDN
###### Downloading Repo
```
cd ~
git clone -b advanced https://github.com/opennetworkinglab/ngsdn-tutorial
```
> If the ngsdn-totorial is already dowloaded before, use this command to update its content.
```
cd ~/ngsdn-tutorial
git pull origin advanced
```
###### Download Dependencies
```
cd ~/ngsdn-tutorial
make deps
```
###### Other Commands
| Make Commands     | Description                              |
|-------------------|------------------------------------------|
|`make deps`        | Pull and build all required dependencies |