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
###### First we have to compile the P4 program: [p4src/main.p4](https://github.com/opennetworkinglab/ngsdn-tutorial/blob/advanced/p4src/main.p4) with this command:
```
cd ~/ngsdn-tutorial
sudo make p4-build
```
###### The output should be the following:
```
*** Building P4 program...
docker run --rm -v /home/sdn/ngsdn-tutorial:/workdir -w /workdir
 opennetworking/p4c:stable \
                p4c-bm2-ss --arch v1model -o p4src/build/bmv2.json \
                --p4runtime-files p4src/build/p4info.txt --Wdisable=unsupported \
                p4src/main.p4
*** P4 program compiled successfully! Output files are in p4src/build
```
###### Now we have to start the mininet topology emulated from the `P4-build`. In order to do that we have to use:
```
sudo make start
```
###### To make sure the topology ran without errors run:
```
sudo make mn-log
```
###### If you get an error because your previosly run it. Use the command `sudo make stop` and start it again or simply use `sudo make restart`.

##### Now in order to run the P4Runtime shell to push the pipeline configuration obtained before. Use the command:
```
sudo util/p4rt-sh --grpc-addr localhost:50001 --config p4src/build/p4info.txt,p4src/build/bmv2.json --election-id 0,1
```
###### If the shell run without errors it shoud display this:
```
*** Connecting to P4Runtime server at host.docker.internal:50001 ...
*** Welcome to the IPython shell for P4Runtime ***
P4Runtime sh >>>
```
###### Now run in another terminal the Mininet CLI using:
```
sudo make mn-cli
```
###### And the output should display:
```
*** Attaching to Mininet CLI...
*** To detach press Ctrl-D (Mininet will keep running)
mininet>
```
###### Now one in the mininet cli we will need to add an NDP entry to h1a and h1b.
```
mininet> h1a ip -6 neigh replace 2001:1:1::B lladdr 00:00:00:00:00:1B dev h1a-eth0
mininet> h1b ip -6 neigh replace 2001:1:1::A lladdr 00:00:00:00:00:1A dev h1b-eth0
```
###### Starting a ping from h1a to h1b. This command should not work sice the table entries have not yet being configure.
```
mininet> h1a ping h1b
```
###### The following commands should be done in the `P4Runtime sh`. This commands are use to insert the following two entries in the `l2_exact_table`. The table below is the fowarding entries we have to implement.
|Match              | Egress Port Number    |
|-------------------|-----------------------|
|`00:00:00:00:00:1B`|4                      |
|`00:00:00:00:00:1A`|3                      |
###### To create the fowarding table:
```
P4Runtime sh >>> te = table_entry["P4INFO-TABLE-NAME"](action = "<P4INFO-ACTION-NAME>")
or
P4Runtime sh >>> te = table_entry["IngressPipeImpl.l2_exact_table"](action = "IngressPipeImpl.set_egress_port")
```
###### To specify the match filed:
```
P4Runtime sh >>> te.match["P4INFO-MATCH-FIELD-NAME"] = ("VALUE")
or 
P4Runtime sh >>> te.match["P4INFO-MATCH-FIELD-NAME"] = ("00:00:00:00:00:1B")
```
###### Now specify the values for the table entry action parameters.
```
P4Runtime sh >>> te.action["P4INFO-ACTION-PARAM-NAME"] = ("VALUE")
```
###### If you want to see what is in the entry object use:
```
P4Runtime sh >>> print(te)
```
###### To insert the entry (wirte in the switch) use:
```
P4Runtime sh >>> te.insert()
```
###### Now if you want to read the table entries from the switch use:
```
P4Runtime sh >>> for te in table_entry["P4INFO-TABLE-NAME"].read():
            ...:     print(te)
            ...:
```
###### After inserting the two entries, try the following comand againg in the Mininet CLI and se h1a communicate with h1b.
```
mininet> h1a ping h1b
PING 2001:1:1::b(2001:1:1::b) 56 data bytes
64 bytes from 2001:1:1::b: icmp_seq=956 ttl=64 time=1.65 ms
64 bytes from 2001:1:1::b: icmp_seq=957 ttl=64 time=1.28 ms
64 bytes from 2001:1:1::b: icmp_seq=958 ttl=64 time=1.69 ms
```
###### I want to give credit of the tutorial to [Open Networking Foundation](https://github.com/opennetworkinglab) where the [ngsdn-tutorial](https://github.com/opennetworkinglab/ngsdn-tutorial) was offered. The tutorial is for their EXCERSISE-1 and it was ran with onos-2.7.0 in May 2022.