## -*- Makefile -*-
## `tests' Subdirectory Makefile for a2ps.
## Copyright (c) 1997-99 Akim Demaille, Miguel Santana
##
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

# .tst instead of .test to avoid tar warnings on MS-DOS

TESTS =		\
align-1.tst	\
backup.tst	\
contrib.tst	\
cut.tst		\
deleg-1.tst	\
deleg-2.tst	\
encoding.tst	\
guess-1.tst	\
guess-2.tst	\
inline.tst	\
inout-1.tst	\
inout-2.tst	\
inout-3.tst	\
options-1.tst	\
pages-1.tst	\
pages-2.tst	\
po.tst		\
printers.tst	\
prolog-1.tst	\
prolog-2.tst	\
strip.tst	\
styles.tst	\
toc.tst		\
usropt-1.tst	\
usropt-2.tst

EXTRA_DIST = $(TESTS) a2ps-tst.cfg.in defs.in \
view-diff ps-ref gps-ref tstfiles

CLEANFILES = ps-chk/* gps-chk/* ps-diff/* gps-diff/*  	\
style.log defs

MAINTAINERCLEANFILES = ps-ref/* gps-ref/*

all-local: defs a2ps-tst.cfg

a2ps-tst.cfg: a2ps-tst.cfg.in
	top_srcdir=`cd $(top_srcdir) && pwd`;	\
	top_builddir=`cd $(top_builddir) && pwd`;	\
	sed -e "s#@libpath@#$$top_builddir/etc:$$top_srcdir/ogonkify:$$top_builddir/ogonkify:$$top_srcdir/sheets:$$top_srcdir/ps:$$top_srcdir/encoding:$$top_srcdir/afm:$$top_builddir/afm:$$top_srcdir/fonts:$$top_srcdir/ppd:$(PSFONT_PATH)#g;s#@file_link@#@FILE_LINK@#g" \
	$(srcdir)/a2ps-tst.cfg.in > a2ps-tst.cfg

DISTCLEANFILES = a2ps-tst.cfg

TESTS_ENVIRONMENT= top_builddir=`cd $(top_builddir) && pwd`
