# Layer 2 Switch
## Before Starting
###### Before starting we must first first setup the controller in the CLI. For this especific example we will be using the following appplications inside the CLI.
```
karaf@root > app activate org.onosproject.openflow
karaf@root > app activate org.onosproject.fwd
```
## Running Layer 2 Switch in the Mininet Terminal
###### To run a simple Layer 2 Switch straight out of terminal. Use the following command line which creates 2 host, 1 switch and 1 remote controller which in this sitaution it will be an controlled by ONOS. 
```
sudo mn --controller remote --switch ovsk,protocols="OpenFlow13"
```
> If you desire a more complex topology use the following command line:
```
sudo mn --controller remote --switch ovsk,protocols="OpenFlow13" --topo tree,depth=3
```
## Running a Layer 2 using a Python script
