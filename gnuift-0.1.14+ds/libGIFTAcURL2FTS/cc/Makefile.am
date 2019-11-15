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
#Makefile for the AcURL2FTS library
#

lib_LTLIBRARIES = libGIFTAcURL2FTS.la

libGIFTAcURL2FTS_la_LDFLAGS="@PRE_INSTALL_LIBDIRS@" -lMRML 
INCLUDES= -DHAS_BOOL -I$(top_srcdir)/libMRML/include -I$(top_srcdir)/libGIFTAcURL2FTS/include \
	-I$(top_srcdir)/expat/xmlparse -I$(top_srcdir)/expat/xmltok 

libGIFTAcURL2FTS_la_SOURCES= \
	CAcURL2FTS.cc\
	CAFURL2FTS.cc\
	plug_in_fo.cc
