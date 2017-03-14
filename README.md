# pacemaker-ryu-bgp

VIPAbgp - An OCF resource for Pacemaker to announce a VIP via BGP:
1. Uses ryu bgp speaker that should be run at every Pacemaker node with rpc on port 50002.
2. No config rewrite/restart required;
3. Does not assign the VIP to interface itself, but default IPaddr2 resource and collocation constraint can be used for that:

### Create VIPAbgp resource:

pcs resource create VIPBGP ocf:heartbeat:VIPAbgp ip=192.168.100.100/32

### Than create IPaddr2 resource:

pcs resource create VIPIP ocf:heartbeat:IPaddr2 params ip=192.168.100.100

### And their collocation:

pcs constraint colocation add VIPBGP with VIPIP

As well as odering constraint will be helpful here:

pcs constraint order VIPIP then VIPBGP kind=Mandatory

## More info:

https://osrg.github.io/ryu/
http://ryu.readthedocs.io/en/latest/library_bgp_speaker_ref.html
