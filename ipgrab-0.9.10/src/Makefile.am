AM_CFLAGS = -Wall -Wstrict-prototypes -Wformat
INCLUDES = -I/usr/local/include

bin_PROGRAMS = ipgrab

ipgrab_SOURCES = ah.h ah.c arp.h arp.c cbcp.h cbcp.c ccp.h ccp.c chap.h chap.c datalink.h datalink.c dhcp.h dhcp.c display.h display.c dns.h dns.c dynports.h dynports.c error.h error.c esp.h esp.c ethernet.h ethernet.c ethertypes.h ethertypes.c file.h file.c ftpctrl.h ftpctrl.c getopt.h getopt.c global.h gre.h gre.c hexbuffer.h hexbuffer.c http.h http.c iana.h iana.c icmp.h icmp.c icmpv6.h icmpv6.c igmp.h igmp.c ip.h ip.c ip_protocols.h ip_protocols.c ip_services.h ip_services.c ipcp.h ipcp.c ipgrab.h ipgrab.c ipv6.h ipv6.c ipx.h ipx.c ipxrip.h ipxrip.c isakmp.h isakmp.c l2tp.h l2tp.c layers.h layers.c lcp.h lcp.c llc.h llc.c local.h loopback.h loopback.c mgcp.h mgcp.c mobileip.h mobileip.c mppc.h mppc.c netbios_ns.h netbios_ns.c nntp.h nntp.c ns_labels.h ns_labels.c open_pcap.h open_pcap.c ospf.h ospf.c packet_manip.h packet_manip.c padding.h padding.c parse_cl.h parse_cl.c payload.h payload.c ppp.h ppp.c pppoe.h pppoe.c pptp.h pptp.c radius.h radius.c radius_3gpp2.h radius_3gpp2.c raw.h raw.c rip.h rip.c ripng.h ripng.c rsvp.h rsvp.c rtcp.h rtcp.c rtp.h rtp.c sdp.h sdp.c sip.h sip.c slip.h slip.c slp.h slp.c ipgsnmp.h snmp.c spx.h spx.c ssh.h ssh.c state.h state.c stats.h stats.c strmap.h strmap.c tcp.h tcp.c tftp.h tftp.c udp.h udp.c utilities.h utilities.c

ipgrab_LDADD = -L/usr/local/lib -lpcap
CLEANFILES = *~
