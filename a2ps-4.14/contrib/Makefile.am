# Makefile for a2ps/contrib.
# Copyright (c) 1995-2000 Akim Demaille, Miguel Santana
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

SUBDIRS = sample emacs

bin_SCRIPTS = card fixps pdiff psmandup psset texi2dvi4a2ps
bin_PROGRAMS = fixnt

fixnt_SOURCES = fixnt.l

EXTRA_DIST = \
card.in fixps.in pdiff.in psmandup.in psset.in texi2dvi4a2ps \
card.m4 fixps.m4 pdiff.m4 psmandup.m4 psset.m4 shell.m4

M4 = @M4@
SUFFIXES = .m4 .in

.m4.in: shell.m4
	$(M4) $*.m4 | \
	  sed -e 's/@BKL@/[/g;s/@BKR@/]/g;s/@DLR@/$$/g;s/@PND@/#/g'>$@-tmp
	mv $@-tmp $@
