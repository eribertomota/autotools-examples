#
# $Id: Makefile.am,v 1.7 2003/09/23 17:48:40 telka Exp $
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

include $(top_srcdir)/../Makefile.rules

SUBDIRS = po

noinst_HEADERS = \
	sysdep.h \
	gettext.h

noinst_LIBRARIES = libbrux.a

libbrux_a_SOURCES = \
	cmd/cmd.c \
	cmd/help.c \
	cmd/quit.c \
	cmd/cmd_detectflash.c \
	flash/cfi.c \
	flash/jedec.c \
	flash/detectflash.c \
	flash/amd.c \
	flash/intel.c
