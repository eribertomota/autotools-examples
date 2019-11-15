# -*- Makefile -*-
# Makefile for a2ps' sources.
# Copyright (c) 1988, 89, 90, 91, 92, 93 Miguel Santana
# Copyright (c) 1995, 96, 97, 98 Akim Demaille, Miguel Santana
#

#
# This file is part of a2ps.
#
# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 3, or (at your option)
# any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; see the file COPYING.  If not, write to
# the Free Software Foundation, 59 Temple Place - Suite 330,
# Boston, MA 02111-1307, USA.
#

## Process this file with automake to produce Makefile.in

## Since this package is written in ansi, be ready to un-ansify
AUTOMAKE_OPTIONS = $(top_builddir)/lib/ansi2knr
localedir = $(datadir)/locale

noinst_PROGRAMS = sample

sample_SOURCES = main.c

INCLUDES = -I. -I.. -I$(top_builddir) -I$(top_srcdir)/intl -I$(top_srcdir)/lib
sample_LDADD = $(top_builddir)/lib/liba2ps.la @LIBINTL@ -lm
DEFS = @DEFS@ -DLOCALEDIR=\"$(localedir)\"
