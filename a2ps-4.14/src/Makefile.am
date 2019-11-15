## Makefile for a2ps' sources.                             -*- Makefile -*-
## Copyright (c) 1988-93 Miguel Santana
## Copyright (c) 1995-99 Akim Demaille, Miguel Santana

##
## This file is part of a2ps.
##
## This program is free software; you can redistribute it and/or modify
## it under the terms of the GNU General Public License as published by
## the Free Software Foundation; either version 3, or (at your option)
## any later version.
##
## This program is distributed in the hope that it will be useful,
## but WITHOUT ANY WARRANTY; without even the implied warranty of
## MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
## GNU General Public License for more details.
##
## You should have received a copy of the GNU General Public License
## along with this program; see the file COPYING.  If not, write to
## the Free Software Foundation, 59 Temple Place - Suite 330,
## Boston, MA 02111-1307, USA.
##

## Process this file with automake to produce Makefile.in

## Since this package is written in ansi, be ready to un-ansify
AUTOMAKE_OPTIONS = $(top_builddir)/lib/ansi2knr

bin_PROGRAMS = a2ps

DEFS = @DEFS@ -DLOCALEDIR=\"$(datadir)/locale\"

a2ps_SOURCES = main.c \
read.c sshread.c ssheet.c select.c generate.c 			\
delegate.c regex.c buffer.c versions.c ffaces.c			\
version-etc.c long-options.c					\
parsessh.y lexssh.l lexps.l sheets-map.l

noinst_HEADERS = main.h \
read.h sshread.h ssheet.h select.h generate.h			\
delegate.h regex.h buffer.h versions.h ffaces.h			\
version-etc.h long-options.h					\
yy2ssh.h lexps.h

BUILT_SOURCES = parsessh.c parsessh.h

YFLAGS = -dtv
LEX = @LEX@
# I don't really understand why I have to put srcdir here, but
# it is needed for yacc and lex files (seems related to #line, but
# I really don't understand why)...
INCLUDES = -I.. -I$(srcdir) -I$(top_srcdir)/lib -I$(top_builddir)/intl

a2ps_LDADD = $(top_builddir)/lib/liba2ps.la @LIBINTL@ -lm

EXTRA_DIST = $(BUILT_SOURCES)
