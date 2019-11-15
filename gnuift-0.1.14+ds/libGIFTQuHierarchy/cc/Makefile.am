#     -*- mode: makefile -*-

#     GIFT, a flexible content based image retrieval system.
#     Copyright (C) 1998, 1999, 2000, 2001, 2002, CUI University of Geneva

#     This program is free software; you can redistribute it and/or modify
#     it under the terms of the GNU General Public License as published by
#     the Free Software Foundation; either version 2 of the License, or
#     (at your option) any later version.

#     This program is distributed in the hope that it will be useful,
#     but WITHOUT ANY WARRANTY; without even the implied warranty of
#     MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#     GNU General Public License for more details.

#     You should have received a copy of the GNU General Public License
#     along with this program; if not, write to the Free Software
#     Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA  02111-1307  USA

#
#Makefile for the QuHierarchy library
#

CCCONFIG=sed -e "s:__EXECBINDIR__:@DEBEXECBINDIR@:g;s:__PERL_LOCATION__:@PERL@:g;s:__BINDIR__:@DEBPERLLIBDIR@:g;s:__DATADIR__:@DEBDATADIR@:g;s:__LIBDIR__:@DEBSHAREDIR@:g;s:__HOME__:${HOME}:g;s:__WEB_PUBLISHING_DIRECTORY__:@WEB_PUBLISHING_DIRECTORY@:g;s=__WEB_PUBLISHING_LOCATION__=@WEB_PUBLISHING_LOCATION@=g;" < $< > $@
#CCCONFIG=sed "s:__PERL_LOCATION__:@PERL@:g;s:__BINDIR__:@bindir@:g;s:__DATADIR__:@datadir@:g" < $< > $@

lib_LTLIBRARIES = libGIFTQuHierarchy.la

libGIFTQuHierarchy_la_LDFLAGS=@PRE_INSTALL_LIBDIRS@ -lMRML -lGIFTAcHierarchy

INCLUDES= -DHAS_BOOL -I$(top_srcdir)/libMRML/include -I$(top_srcdir)/libGIFTAcHierarchy/include -I$(top_srcdir)/libGIFTQuHierarchy/include

libGIFTQuHierarchy_la_SOURCES= CQHierarchy.cc plug_in_fo.cc
