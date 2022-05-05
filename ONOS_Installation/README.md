# Installation of ONOS
## Requirements
###### ONOS shouldn't run as a root since it is a production service. Scripts used by ONOs need to run as a service requires a unprivilaged user. This often written as 'sdn'.
```
sudo adduser sdn --system --group
```