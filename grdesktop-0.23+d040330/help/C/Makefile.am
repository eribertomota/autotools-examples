## grdesktop - gtk rdesktop frontend
## Copyright (C) 2002 Thorsten Sauter <tsauter@gmx.net>
##
## $Id: Makefile.am,v 1.5 2004/03/30 13:56:57 tsauter Exp $
##
## This program is free software; you can redistribute it and/or modify
## it under the terms of the GNU General Public License as published by
## the Free Software Foundation; either version 2 of the License, or
## (at your option) any later version.
##
## This program is distributed in the hope that it will be useful,
## but WITHOUT ANY WARRANTY; without even the implied warranty of
## MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
## GNU General Public License for more details.
##
## You should have received a copy of the GNU General Public License
## along with this program; if not, write to the Free Software
## Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA  02111-1307  USA
##


figs = $(top_srcdir)/pixmaps/grdesktop-mainwin.png
docname = grdesktop
lang = C
extraomf =
omffile =
entities = legal.xml

include $(top_srcdir)/help/xmldocs.make

omf_timestamp: $(omffile)
	-for file in $(omffile); do \
		scrollkeeper-preinstall $(docdir)/$(docname).xml $(srcdir)/$$file $$file.out; \
	done
	-for file in $(extraomf); do \
		scrollkeeper-preinstall $(docdir)/`echo $$file | cut -f1 -d -`.xml $(srcdir)/$$file $$file.out; \
	done
	touch omf_timestamp

install-data-hook-omf:
	-scrollkeeper-update -p $(scrollkeeper_localstate_dir) -o $(DESTDIR)$(omf_dest_dir)

dist-hook: app-dist-hook

EXTRA_DIST += $(extraomf)

