#
#      Makefile.am from Wireless Access Point Utilites for Unix
#
#  Copyright (c) 2002 Roman Festchook <roma at polesye dot net>
#
#  This program is free software; you can redistribute it and/or modify
#  it under the terms of the GNU General Public License Version 2 from
#  June 1991 as published by the Free Software Foundation.
#
#  This program is distributed in the hope that it will be useful, but
#  WITHOUT ANY WARRANTY; without even the implied warranty of
#  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#  GNU General Public License for more details.
#
#  You should have received a copy of the GNU General Public License along
#  with this program; if not, write to the Free Software Foundation, Inc.,
#  59 Temple Place, Suite 330, Boston, MA 02111-1307 USA
#

DEFS = -DLOCALEDIR=\"$(datadir)/locale\" -DHAVE_CONFIG_H
INCLUDES = -I../lib -I../intl -I..
LIBS = @INTLLIBS@ @LIBS@

bin_PROGRAMS = ap-config ap-mrtg ap-auth ap-tftp ap-rrd
sbin_PROGRAMS = ap-trapd
 
ap_config_SOURCES = ap-config.c auth.c bridge.c nwn_advanced.c nwn_latest.c stations.c aplink.c
ap_config_LDADD = ../lib/libap.a -lmenu @CURSESLIBS@

ap_tftp_SOURCES = ap-tftp.c
ap_tftp_LDADD = ../lib/libap.a

ap_trapd_SOURCES = ap-trapd.c

ap_auth_SOURCES = ap-auth.c
ap_auth_LDADD = ../lib/libap.a

ap_mrtg_SOURCES = ap-mrtg.c
ap_mrtg_LDADD = ../lib/libap.a

ap_rrd_SOURCES = ap-rrd.c
ap_rrd_LDADD = ../lib/libap.a

