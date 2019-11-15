#
# Makefile.am for libhfsp/test
# Created by Klaus Kaempf <kkaempf@suse.de>
#
#
# libhfsp+ - library for reading and writing Macintosh HFS+ volumes
# Copyright (C) 1996-1998 Robert Leslie
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
# $Id: Makefile.am,v 1.1.1.1 2002/03/05 19:50:29 klaus Exp $
#

testdir = .
test_PROGRAMS = hfsptest
hfsptest_SOURCES = test.c
hfsptest_LDADD = ../src/libhfsp.la

INCLUDES = -I../src

clean-local:
	rm -f hfsptest

EXTRA_DIST = volumes
