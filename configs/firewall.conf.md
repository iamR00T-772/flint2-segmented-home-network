# Sanitized excerpt from /etc/config/firewall
# Sensitive identifiers have been intentionally redacted.

config defaults
	option input 'ACCEPT'
	option output 'ACCEPT'
	option forward 'REJECT'
	option synflood_protect '1'

config rule 'lan_drop_leaked_adgdns'
	option name 'lan_drop_leaked_adgdns'
	option src 'lan'
	option proto 'udp'
	option dest_port '3053'
	option mark '0x0/0xf000'
	option target 'DROP'

config rule 'lan_drop_leaked_dns'
	option name 'lan_drop_leaked_dns'
	option src 'lan'
	option proto 'udp'
	option dest_port '53'
	option mark '!0x8000/0xf000'
	option target 'DROP'

config rule 'iot_drop_leaked_adgdns'
	option name 'iot_drop_leaked_adgdns'
	option src 'iot'
	option proto 'udp'
	option dest_port '3053'
	option mark '0x0/0xf000'
	option target 'DROP'

config rule 'iot_drop_leaked_dns'
	option name 'iot_drop_leaked_dns'
	option src 'iot'
	option proto 'udp'
	option dest_port '53'
	option mark '!0x8000/0xf000'
	option target 'DROP'

config rule 'guest_drop_leaked_adgdns'
	option name 'guest_drop_leaked_adgdns'
	option src 'guest'
	option proto 'udp'
	option dest_port '3053'
	option mark '0x0/0xf000'
	option target 'DROP'

config rule 'guest_drop_leaked_dns'
	option name 'guest_drop_leaked_dns'
	option src 'guest'
	option proto 'udp'
	option dest_port '53'
	option mark '!0x8000/0xf000'
	option target 'DROP'

config zone
	option name 'lan'
	option input 'ACCEPT'
	option output 'ACCEPT'
	option forward 'ACCEPT'
	list network 'lan'

config zone
	option name 'wan'
	list network 'wan'
	list network 'wan6'
	list network 'wwan'
	list network 'secondwan'
	option output 'ACCEPT'
	option forward 'REJECT'
	option masq '1'
	option mtu_fix '1'
	option input 'DROP'

config forwarding
	option src 'lan'
	option dest 'wan'
	option enabled '1'

config rule
	option name 'Allow-DHCP-Renew'
	option src 'wan'
	option proto 'udp'
	option dest_port '68'
	option target 'ACCEPT'
	option family 'ipv4'

config rule
	option name 'Allow-IGMP'
	option src 'wan'
	option proto 'igmp'
	option family 'ipv4'
	option target 'ACCEPT'

config rule
	option name 'Allow-DHCPv6'
	option src 'wan'
	option proto 'udp'
	option dest_port '546'
	option family 'ipv6'
	option target 'ACCEPT'

config rule
	option name 'Allow-MLD'
	option src 'wan'
	option proto 'icmp'
	option src_ip 'fe80::/10'
	list icmp_type '130/0'
	list icmp_type '131/0'
	list icmp_type '132/0'
	list icmp_type '143/0'
	option family 'ipv6'
	option target 'ACCEPT'

config rule
	option name 'Allow-ICMPv6-Input'
	option src 'wan'
	option proto 'icmp'
	option limit '1000/sec'
	option family 'ipv6'
	option target 'ACCEPT'
	list icmp_type 'destination-unreachable'
	list icmp_type 'packet-too-big'
	list icmp_type 'time-exceeded'
	list icmp_type 'bad-header'
	list icmp_type 'unknown-header-type'
	list icmp_type 'router-solicitation'
	list icmp_type 'neighbour-solicitation'
	list icmp_type 'router-advertisement'
	list icmp_type 'neighbour-advertisement'

config rule
	option name 'Allow-ICMPv6-Forward'
	option src 'wan'
	option dest '*'
	option proto 'icmp'
	option limit '1000/sec'
	option family 'ipv6'
	option target 'ACCEPT'
	list icmp_type 'destination-unreachable'
	list icmp_type 'packet-too-big'
	list icmp_type 'time-exceeded'
	list icmp_type 'bad-header'
	list icmp_type 'unknown-header-type'

config rule
	option name 'Allow-IPSec-ESP'
	option src 'wan'
	option dest 'lan'
	option proto 'esp'
	option target 'ACCEPT'

config rule
	option name 'Allow-ISAKMP'
	option src 'wan'
	option dest 'lan'
	option dest_port '500'
	option proto 'udp'
	option target 'ACCEPT'

config rule
	option name 'Support-UDP-Traceroute'
	option src 'wan'
	option dest_port '33434:33689'
	option proto 'udp'
	option family 'ipv4'
	option target 'REJECT'
	option enabled '0'

config include
	option path '/etc/firewall.user'

config zone
	option name 'guest'
	option network 'guest'
	option forward 'REJECT'
	option output 'ACCEPT'
	option input 'REJECT'

config forwarding
	option src 'guest'
	option dest 'wan'
	option enabled '1'

config rule
	option name 'Allow-DHCP'
	option src 'guest'
	option target 'ACCEPT'
	option proto 'udp'
	option dest_port '67-68'

config rule
	option name 'Allow-DNS'
	option src 'guest'
	option target 'ACCEPT'
	option proto 'tcp udp'
	option dest_port '53'

config zone
	option name 'iot'
	option network 'iot'
	option forward 'REJECT'
	option output 'ACCEPT'
	option input 'REJECT'

config forwarding
	option src 'iot'
	option dest 'wan'

config rule
	option name 'Allow-DHCP'
	option src 'iot'
	option target 'ACCEPT'
	option proto 'udp'
	option dest_port '67-68'

config rule
	option name 'Allow-DNS'
	option src 'iot'
	option target 'ACCEPT'
	option proto 'tcp udp'
	option dest_port '53'

config include 'nat6'
	option path '/etc/firewall.nat6'
	option reload '1'

config include 'dns_order'
	option type 'script'
	option path '/etc/firewall.dns_order'
	option reload '1'
	option enabled '1'

config include
	option enabled '1'
	option type 'script'
	option path '/etc/netifyd/iptables-init.sh'
	option reload '1'
	option fw4_compatible '1'

config include 'vpnclient'
	option type 'script'
	option path '/usr/bin/rtp2.sh'
	option reload '0'

config include 'glblock'
	option type 'script'
	option path '/usr/bin/gl_block.sh'
	option reload '1'

config include 'security'
	option type 'script'
	option path '/etc/firewall.security'
	option reload '1'

config include
	option type 'script'
	option path '/etc/firewall.pf'
	option reload '0'

config zone
	option name 'gaming'
	option input 'REJECT'
	option output 'ACCEPT'
	option forward 'REJECT'
	list network 'gaming'

config zone
	option name 'siem'
	option input 'REJECT'
	option output 'ACCEPT'
	option forward 'REJECT'
	list network 'siem'

config zone
	option name 'tv'
	option input 'REJECT'
	option output 'ACCEPT'
	option forward 'REJECT'
	list network 'tv'

config forwarding
	option src 'gaming'
	option dest 'wan'

config forwarding
	option src 'siem'
	option dest 'wan'

config forwarding
	option src 'tv'
	option dest 'wan'

config rule
	option name 'Allow-DHCP-gaming'
	list proto 'udp'
	option src 'gaming'
	option dest_port '67-68'
	option target 'ACCEPT'

config rule
	option name 'Allow-DNS-gaming'
	option src 'gaming'
	option dest_port '53'
	option target 'ACCEPT'

config rule
	option name 'Allow-DHCP-siem'
	list proto 'udp'
	option src 'siem'
	option dest_port '67-68'
	option target 'ACCEPT'

config rule
	option name 'Allow-DNS-siem'
	option src 'siem'
	option dest_port '53'
	option target 'ACCEPT'

config rule
	option name 'Allow-DHCP-tv'
	list proto 'udp'
	option src 'tv'
	option dest_port '67-68'
	option target 'ACCEPT'

config rule
	option name 'Allow-DNS-tv'
	option src 'tv'
	option dest_port '53'
	option target 'ACCEPT'

config rule 'glnas_ser'
	option src 'wan'
	option dest_port '6000-6002'
	option dest_proto 'tcp'
	option target 'DROP'

config rule 'webdav_wan'
	option src 'wan'
	option dest_port '6008'
	option dest_proto 'tcp'
	option target 'DROP'

config rule 'tcp_dns_leak_drop'
	option name 'tcp_dns_leak_drop'
	option proto 'tcp'
	option family 'any'
	option mark '0x0/0xf000'
	option target 'DROP'
	option extra '-m owner --uid-owner 453'
	option enabled '1'

config zone 'wgclient1'
	option name 'wgclient1'
	option forward 'ACCEPT'
	option output 'ACCEPT'
	option mtu_fix '1'
	option network 'wgclient1'
	option input 'DROP'
	option masq '1'
	option masq6 '1'
	option enabled '1'
	option gl_vpn_rules '1'

config forwarding 'lan2wgclient1'
	option src 'lan'
	option dest 'wgclient1'
	option gl_vpn_rules '1'

config forwarding 'iot2wgclient1'
	option src 'iot'
	option dest 'wgclient1'
	option gl_vpn_rules '1'

config forwarding 'guest2wgclient1'
	option src 'guest'
	option dest 'wgclient1'
	option gl_vpn_rules '1'