# dhcp-bind-ddns-working-setup
Example configuration Files for Bind9 and ISC DHCP setup with DDNS updates. 
Hidden Bind master with NS1 and NS2 nameservers
DHCP failover Peer setup with NS1 as primary and NS2 as secondary

Setup:

Bind Master:
1. Install Bind9
2. Use master/bind/named.conf configuration files as a guide to setup bind

NS1 slave:
1. Install Bind9
2. Use master/bind/named.conf* configuration files as a guide to setup bind NS1. [Change IP addresses as per your network subnet]
3. Install ISC-DHCP-server
4. Use master/dhcp/dhcpd.conf configuration files as a guide to setup dhcp primary peer. [Change IP addresses as per your network subnet]

NS2 slave:
1. Install Bind9
2. Use master/bind/named.conf* configuration files as a guide to setup bind NS2. [Change IP addresses as per your network subnet]
3. Install ISC-DHCP-server
4. Use master/dhcp/dhcpd.conf configuration files as a guide to setup dhcp secondary peer. [Change IP addresses as per your network subnet]

Testing:
1. After setup, restart Bind9 on Master. Bind 9 and DHCP on slaves: 
> named-checkconf
> service bind9 restart
> dhcpd -t
> service isc-dhcp-server restart
2. Check syslogs to verify everything is working fine
3. Add a node on your network and check syslogs for DDNS updates sent to Master.
4. "dig <node_hostname>.<network_domain>" on master, ns1, ns2 to verify ddns is working. 
