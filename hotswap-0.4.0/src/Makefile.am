## backend/Makefile.am
##
## Copyright (C) 2002 Tim Stadelmann
##
## This program is free software; you can redistribute it and/or modify
## it under the terms of the GNU General Public License as published by
## the Free Software Foundation; either version 2, or (at your option)
## any later version.
##
## This program is distributed in the hope that it will be useful,
## but WITHOUT ANY WARRANTY; without even the implied warranty of
## MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
## GNU General Public License for more details.
##
## You should have received a copy of the GNU General Public License
## along with this program; if not, write to the Free Software Foundation,
## Inc., 59 Temple Place - Suite 330, Boston, MA 02111-1307, USA.  

datadir = @datadir@
localedir = $(datadir)/locale
DEFS = -DLOCALEDIR=\"$(localedir)\" @DEFS@

INCLUDES = -I. -I.. -I../intl @XML_CFLAGS@

bin_PROGRAMS=hotswap

hotswap_SOURCES = hotswap.c hotswap.h
EXTRA_hotswap_SOURCES = rcfile.c rcfile.h
hotswap_LDADD = $(INTLLIBS) @RCFILE@ @XML_LIBS@
hotswap_DEPENDENCIES = @RCFILE@

#  Make the installed program setuid root.
install-exec-hook:
	chown root $(bindir)/hotswap
	chmod u+s $(bindir)/hotswap
