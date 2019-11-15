## Top level Makefile for a2ps.
## Copyright (C) 1995-2007 Akim Demaille, Miguel Santana and Masayuki Hatta
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
## along with this program; if not, write to the Free Software
## Foundation, Inc., 59 Temple Place - Suite 330, Boston, MA 02111-1307, USA.

## Process this file with automake to produce Makefile.in
AUTOMAKE_OPTIONS = check-news 1.6.3 dist-bzip2 readme-alpha

## Make sure to drop doc at the end: it causes may problems, so
## let's do the maximum before it
SUBDIRS = auxdir m4 etc ps ogonkify \
	lib src po tests sheets encoding afm fonts ppd contrib doc man

ACLOCAL_AMFLAGS = -I m4
EXTRA_DIST = TODO ANNOUNCE FAQ a2ps.prj arch

MAKE_AUTHORS = make-authors.pl

## I shouldn't need this, it looks like a bug in Automake
AMTAR = @AMTAR@
AMTARFLAGS = @AMTARFLAGS@
PERL = @PERL@
all-local: FAQ AUTHORS

prcs-diff:
	thisver=`echo "Version-$(VERSION)" | sed 's/\./-/g'`; \
	IFS="${IFS}:,;" ; \
	for prev in $(PREV); \
	do \
	  prevno=`echo "$$prev" | sed 's/^\./0./'`; \
	  prevver=Version-`echo $$prevno | sed 's/\./-/g'`; \
	  diff=$(PACKAGE)-$$prevno-$(VERSION).diff; \
	  prcs diff -r $$prevver -r $$thisver -N $(PACKAGE) -- -u > $$diff; \
	  gzip -c $$diff > $$diff.gz && \
	  bzip2 $$diff ;\
	done

FAQ: $(top_srcdir)/doc/a2ps.texi
	LC_ALL=C $(MAKEINFO) --no-header -I $(top_srcdir)/doc a2ps.texi | \
	sed -n -f $(top_srcdir)/auxdir/make-faq.sed > FAQ-tmp
	mv FAQ-tmp FAQ

AUTHORS: $(top_srcdir)/doc/translators.txt $(top_srcdir)/doc/$(MAKE_AUTHORS) $(top_srcdir)/sheets/sheets.map
	cd doc \
	&& $(PERL) $(MAKE_AUTHORS) > $@-t \
	&& chmod 644 $@-t
	mv doc/$@-t $@
