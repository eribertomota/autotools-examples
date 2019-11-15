## grdesktop - gtk rdesktop frontend
## Copyright (C) 2002 Thorsten Sauter <tsauter@gmx.net>
##
## $Id: Makefile.am,v 1.25 2004/03/02 13:25:15 tsauter Exp $
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


bin_PROGRAMS = grdesktop

INCLUDES = -I$(top_srcdir) -I$(top_builddir) \
	-I$(top_srcdir)/intl \
	$(GTK_CFLAGS) \
	-DDATADIR=\""$(datadir)"\" \
	-DLOCALEDIR=\""$(datadir)/locale"\" \
	-DKBPATH=\""$(kbpath)"\"

grdesktop_LDFLAGS = -export-dynamic
grdesktop_SOURCES = main.c main.h \
	srvsel.c srvsel.h \
	run.c run.h \
	btnbox.c btnbox.h \
	optbox.c optbox.h \
	options.c options.h \
	rdpparse.c rdpparse.h \
	sshbox.c sshbox.h \
	config.h

grdesktop_LDADD = $(GTK_LIBS)

grdesktopdir = $(datadir)/applications
grdesktop_DATA = grdesktop.desktop

gsettings_SCHEMAS = org.nongnu.grdesktop.gschema.xml

@GSETTINGS_RULES@

install-data-local:
	if test -z "$(DESTDIR)"; then \
		GCONF_CONFIG_SOURCE=$(GCONF_SCHEMA_CONFIG_SOURCE) $(GCONFTOOL) --makefile-install-rule $(schema_source_data); \
	fi

EXTRA_DIST = \
	$(grdesktop_DATA) \
	$(gsettings_SCHEMAS)

