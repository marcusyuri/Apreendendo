# Learning
```
git clone https://github.com/marcusyuri/Apreendendo.git
ncs-make-package --no-java --no-python --netconf-ned Apreendendo/src/yang/ openconfig-ned
cd openconfig-ned/src/
make
cd ..
ncs-netsim create-network openconfig 1 router
ncs-netsim start
ncs-netsim cli-i router0
```

## Use Case: Flat Switch, VLAN-aware L2VPN, or Virtual Switch
This is an example using netconf-cli on how to configurate and openconfig device

```
nso-cross-compiler> ena
nso-cross-compiler# configure
Enter configuration commands, one per line. End with CNTL/Z.
router0(config)#interfaces interface g0/0/0 config name g0/0/0 type IF_ETHERNET
router0(config-interface-g0/0/0)#ethernet switched-vlan config interface-mode ACCESS
router0(config-interface-g0/0/0)#ethernet switched-vlan config access-vlan 1042
router0(config-interface-g0/0/0)#config description "ACCESS PORT"
router0(config-interface-g0/0/0)#ex
router0(config)#interfaces interface g1/0/42 config name g1/0/42 type IF_ETHERNET
router0(config-interface-g1/0/42)#config description "TRUNK PORT"
router0(config-interface-g1/0/42)#ethernet switched-vlan config interface-mode TRUNK
router0(config-interface-g1/0/42)#ethernet switched-vlan config trunk-vlans 2048
router0(config-interface-g1/0/42)#ethernet switched-vlan config trunk-vlans 2049
router0(config-interface-g1/0/42)#top
router0(config)#network-instances network-instance DEFAULT config name DEFAULT type DEFAULT_INSTANCE
router0(config-network-instance-DEFAULT)#interfaces interface g0/0/0 config id g0/0/0
router0(config-interface-g0/0/0)#config interface ?
Possible completions:
  g0/0/0  g1/0/42
router0(config-interface-g0/0/0)#config interface g0/0/0
router0(config-interface-g0/0/0)#exit
router0(config-network-instance-DEFAULT)#interfaces interface g1/0/42 config id g1/0/42
router0(config-interface-g1/0/42)#config interface g1/0/42
router0(config-interface-g1/0/42)#exit
router0(config-network-instance-DEFAULT)#vlans vlan 2048 config vlan-id 2048
router0(config-vlan-2048)#config name GREEN
router0(config-vlan-2048)#exit
router0(config-network-instance-DEFAULT)#vlans vlan 2049 config vlan-id 2049
router0(config-vlan-2049)#config name ORANGE
router0(config-vlan-2049)#exit
router0(config-network-instance-DEFAULT)#vlans vlan 1042 config vlan-id 1042
router0(config-vlan-1042)#config name RED
router0(config-vlan-1042)#
```
