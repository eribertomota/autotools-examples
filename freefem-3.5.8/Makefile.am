# -*- Mode: makefile  -*-
#
# $Id: Makefile.am,v 1.9 2001/10/20 23:57:16 prudhomm Exp $
#
# SUMMARY:      
# USAGE:        make <make-target>
#
# AUTHOR:       Christophe Prud'homme
# ORG:           
# E-MAIL:       prudhomm@users.sourceforge.net
#
# ORIG-DATE:     2-Nov-96 at 03:56:10
# LAST-MOD: 20-Oct-01 at 19:54:17 by Christophe Prud'homme
#
# DESCRIPTION:  
#  This program is free software; you can redistribute it and/or modify
#  it under the terms of the GNU General Public License as published by
#  the Free Software Foundation; either version 2 of the License, or
#  (at your option) any later version.
# 
#  This program is distributed in the hope that it will be useful,
#  but WITHOUT ANY WARRANTY; without even the implied warranty of
#  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#  GNU General Public License for more details.
#  
#  You should have received a copy of the GNU General Public License
#  along with this program; if not, write to the Free Software
#  Foundation, Inc., 675 Mass Ave, Cambridge, MA 02139, USA.
#
#
#  - Look in GNU Coding standards for further informations
#
# DESCRIP-END.	

AUTOMAKE_OPTIONS=check-news 

host		= @host@

SUBDIRS		= admin doc freefem freefem-api examples 

DATA_SUBDIRS	= examples freefem-api

EXTRA_DIST	= FAQ GNUINSTALL freefem.spec.in Makefile.cvs freefem.doxygen
data_DATA	= ChangeLog README NEWS TODO
datadir		= $(prefix)/share/doc/$(PACKAGE)/


$(ACLOCAL_M4):  configure.in  
	cd $(srcdir) && $(ACLOCAL) -I admin

freefem.spec: freefem.spec.in

doc:
	doxygen freefem.doxygen

rpm: freefem.spec
	make dist
	cp freefem-@VERSION@.tar.gz /usr/src/redhat/SOURCES
	rpm -bb freefem.spec
# now the rpm are in /usr/src/redhat/RPMS/<arch>/
# some cleanup
	rm /usr/src/redhat/SOURCES/freefem-@VERSION@.tar.gz
