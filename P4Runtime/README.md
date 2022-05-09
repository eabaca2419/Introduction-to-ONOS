# P4Runtime Basics
###### Before we start doing a simple P4 code connection we must first install sveral system requirements. Most of them should be al ready downloaded except docker which is the most important application from all the other dependencies.
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
sudo make deps
```
###### Other Commands
| Make Commands     | Description                                           |
|-------------------|-------------------------------------------------------|    
|`make deps`        | Pull and build all required dependencies              |
|`make p4-build`    | Build P4 Program                                      |
|`make p4-test`     | Run PTF test                                          |
|`make start`       | Start Mininet and ONOS containers                     |
|`make stop`        | Stop all containers                                   |
|`make restart`     | Restart containers clearing any previous state        |
|`make onos-cli`    | Access the ONOS CLI (password: rocks, Ctrl-D to exit) |
|`make onos-log`    | Show ONOS log                                         |
|`make mn-cli`      | Access the Mininet CLI (Ctrl-D to exit)               |
|`make mn-log`      | Show Mininet log                                      |
|`make app-build`   | Build custom ONOS app                                 |
|`make app-reload`  | Install and activate the ONOS app                     |
|`make netcfg`      | Push netcfg.json file (network config) to ONOS        |
## P4Runtime Basic
