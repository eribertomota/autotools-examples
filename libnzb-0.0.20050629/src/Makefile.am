#  libnzb
#
#  Copyright (C) 2004 Mattias Nordstrom <matta at ftlight net>
#
#  This program is free software; you can redistribute it and/or modify
#  it under the terms of the GNU General Public License as published by
#  the Free Software Foundation; either version 2 of the License, or
#  (at your option) any later version.
#
#  This program is distributed in the hope that it will be useful,
#  but WITHOUT ANY WARRANTY; without even the implied warranty of
#  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#  GNU General Public License for more details.
#
#  You should have received a copy of the GNU General Public License
#  along with this program; if not, write to the Free Software
#  Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA  02111-1307  USA
#
#
#  Authors:
#    Mattias Nordstrom <matta at ftlight net>
#
#  $Id: Makefile.am,v 1.2 2005/02/27 20:35:54 mnordstr Exp $
#    Makefile.am


lib_LTLIBRARIES = libnzb.la
libnzb_la_SOURCES = nntp.cpp yenc.cpp uenc.cpp crc32.c nzb.cpp nntp.h yenc.h uenc.h crc32.h nzb.h
libnzb_la_LIBADD =
libnzb_la_LDFLAGS = -version-info 0:0:0 `xml2-config --libs`

#bin_PROGRAMS = libnzb
#libnzb_SOURCES = main.cpp nntp.cpp yenc.cpp crc32.c nzb.cpp nntp.h yenc.h crc32.h nzb.h
#libnzb_LDADD = 
#libnzb_LDFLAGS = `xml2-config --libs`

CPPFLAGS = -Wall `xml2-config --cflags`

INCLUDES = -I$(top_builddir) -I$(top_srcdir)

SUBDIRS =
