# CLI
## Commands Inside the CLI
###### See what app are active iside your CLI
```
karaf@root > apps -a -s
```
###### OpenFlow
> OpenFlow is a protocol that allows a server to tell network switches where to send packets. If you wan to make you network using a OpenFlow controller, use the follwoing line inside the cli. 
```
karaf@root > app activate org.onosproject.openflow
```
###### Reactive Fowarding
> Pings in mininet will now work if you have not activated the *Reactive Fowarding* app.
```
karaf@root > app activate org.onosproject.fwd
```
###### If you want to see more useful commands go to the [ONOS-Wiki](https://wiki.onosproject.org/display/ONOS/Appendix+A+%3A+CLI+commands)