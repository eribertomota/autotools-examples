# Makefile.am for libhfsp/src, used by automake
# Created by Klaus Kaempf <kkaempf@suse.de>
#
# Copyright (C) 2000 Klaus Halfmann <klaus.halfmann@feri.de>
# Original code 1996-1998 by Robert Leslie <rob@mars.rog>
# other work 2000 from Brad Boyer (flar@pants.nu)
#
# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 2 of the License, or
# (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 675 Mass Ave, Cambridge, MA 02139, USA.
#
# $Id: Makefile.am,v 1.2 2002/03/08 21:15:52 klaus Exp $
#

lib_LTLIBRARIES = libhfsp.la
libhfsp_la_SOURCES =	\
	    blockiter.c btree.c btreecheck.c fscheck.c hfstime.c libhfsp.c os.c unicode.c \
	    record.c volume.c partitions.c 

CFLAGS = -O2 -Wall

# I need to clean up these headers first before i can distribute them ...		
# include_HEADERS = apple.h hfs.h hfsp.h libhfsp.h 
