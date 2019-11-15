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

bin_PROGRAMS = ap-gl
 
ap_gl_SOURCES = ap-gl.c auth.c bridge.c stations.c
ap_gl_LDADD = ../lib/libap.a -lmenu @CURSESLIBS@

