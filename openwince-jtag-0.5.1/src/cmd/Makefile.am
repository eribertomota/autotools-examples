#
# $Id: Makefile.am,v 1.12 2003/09/05 21:09:14 telka Exp $
#
# Copyright (C) 2003 ETC s.r.o.
#
# This program is free software; you can redistribute it and/or
# modify it under the terms of the GNU General Public License
# as published by the Free Software Foundation; either version 2
# of the License, or (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 59 Temple Place - Suite 330, Boston, MA
# 02111-1307, USA.
#
# Written by Marcel Telka <marcel@telka.sk>, 2003.
#

include $(top_srcdir)/Makefile.rules

noinst_LIBRARIES = libcmd.a

libcmd_a_SOURCES = \
	frequency.c \
	cable.c \
	discovery.c \
	detect.c \
	signal.c \
	bit.c \
	register.c \
	initbus.c \
	print.c \
	part.c \
	bus.c \
	instruction.c \
	shift.c \
	dr.c \
	get.c \
	set.c \
	endian.c \
	peekpoke.c \
	readmem.c \
	flashmem.c \
	eraseflash.c \
	script.c \
	include.c \
	cmd.c

INCLUDES = -DJTAG_DATA_DIR=\"$(pkgdatadir)\"
