# Learning
```
git clone https://github.com/marcusyuri/Apreendendo.git
ncs-make-package --no-java --netconf-ned Apreendendo/src/yang/ openconfig-ned
cd openconfig-ned/src/
make
cd ..
ncs-netsim create-network openconfig 1 router
ncs-netsim start
ncs-netsim cli-i router0
```
