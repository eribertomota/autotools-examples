#
#      Makefile.am from Access Point SNMP Utils for Linux
#
#  Copyright (c) 2002 Roman Festchook <roma at polesye dot net>
#
#  This program is free software; you can redistribute it and/or modify
#  it under the terms of the GNU General Public License Version 2 from
#  June 1991 as published by the Free Software Foundation.
#
#  This program is distributed in the hope that it will be useful, but
#  WITHOUT ANY WARRANTY; without even the implied warranty of
#  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#  GNU General Public License for more details.
#
#  You should have received a copy of the GNU General Public License along
#  with this program; if not, write to the Free Software Foundation, Inc.,
#  59 Temple Place, Suite 330, Boston, MA 02111-1307 USA
#

## Process this file with automake to produce Makefile.in

SUBDIRS = lib src ap-gl Documentation intl po

AUTOMAKE_OPTIONS = gnu 

EXTRA_DIST = config/* ap-utils.spec

dist-hook:
	rm -f $(distdir)/po/*.gmo
	-chmod -R a+r $(distdir)
	tar chof $(distdir).tar $(distdir)
	bzip2 -v9f $(distdir).tar
