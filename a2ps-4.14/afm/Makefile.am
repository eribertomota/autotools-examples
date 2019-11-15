# -*- Makefile -*-
# Makefile for a2ps' AFM library directory.
#
# Copyright (c) 1988, 89, 90, 91, 92, 93 Miguel Santana
# Copyright (c) 1995, 96, 97, 98 Akim Demaille, Miguel Santana
#
# $Id: Makefile.am,v 1.1.1.1.2.2 2007/12/29 01:58:10 mhatta Exp $
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

A2PS = $(top_builddir)/src/a2ps
A2PS_CONFIG = $(top_builddir)/tests/a2ps-tst.cfg

# As a new `feature' :), a2ps uses now even more directories
afmdir = $(pkgdatadir)/afm

pcg_afms = pcfont.afm

level1_afms = \
pcrb.afm pcrbo.afm pcrr.afm pcrro.afm	\
phvb.afm phvbo.afm phvr.afm phvro.afm 	\
ptmb.afm ptmbi.afm ptmi.afm ptmr.afm	\
psyr.afm

level2_afms = \
pagb.afm pagbo.afm pagd.afm pagdo.afm \
pbkd.afm pbkdi.afm pbkl.afm pbkli.afm		\
phvbon.afm phvbrn.afm phvron.afm phvrrn.afm	\
pncb.afm pncbi.afm pncr.afm pncri.afm		\
pplb.afm pplbi.afm pplr.afm pplri.afm 		\
pzcmi.afm pzdr.afm

all_afms = $(pcg_afms) $(level1_afms) $(level2_afms)

if EXTENSIONS
afm_DATA = fonts.map $(all_afms)
afm_SCRIPTS = make_fonts_map.sh
else
afm_DATA = fonts.map $(level1_afms)
endif

EXTRA_DIST = $(all_afms) make_fonts_map.sh fontsmap
DISTCLEANFILES = fonts.map

# FIXME: touch fonts.map
# It is needed because a2ps cannot run if it cannot find a fonts.map
# file, and since we need a2ps so that it tells us its path, we create
# an empty fonts.map just for the time of the configuration
fonts.map: $(srcdir)/make_fonts_map.sh $(A2PS_CONFIG)
	. $(top_builddir)/tests/defs ;\
	touch fonts.map ; \
	if $(SHELL) $(srcdir)/make_fonts_map.sh > /dev/null; then \
	  mv fonts.map.new fonts.map ;\
	else \
	  echo "Failed to build a fonts.map file."; \
	  echo "Reverting to default file."; \
	  cp $(srcdir)/fontsmap fonts.map; \
	fi
