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
#Makefile for the inverted File library
#

CCCONFIG=sed "s:__EXECBINDIR__:@DEBEXECBINDIR@:g;s:__PERL_LOCATION__:@PERL@:g;s:__BINDIR__:@DEBPERLLIBDIR@:g;s:__DATADIR__:@DEBDATADIR@:g;s:__LIBDIR__:@DEBSHAREDIR@:g;s:__HOME__:${HOME}:g;s:__WEB_PUBLISHING_DIRECTORY__:@WEB_PUBLISHING_DIRECTORY@:g;s=__WEB_PUBLISHING_LOCATION__=@WEB_PUBLISHING_LOCATION@=g;" < $< > $@

lib_LTLIBRARIES = libGIFTAcInvertedFile.la

libGIFTAcInvertedFile_la_LDFLAGS= -module "@PRE_INSTALL_LIBDIRS@" -lMRML -lGIFTAcURL2FTS

INCLUDES= -DHAS_BOOL -I$(top_srcdir)/libMRML/include -I$(top_srcdir)/libGIFTAcInvertedFile/include -I$(top_srcdir)/libGIFTAcURL2FTS/include 


#CAcIFFileSystem.cc: CAcIFFileSystem.pre-cc
#	$(CCCONFIG)

# libGIFTInvertedFile_a_SOURCES= 
libGIFTAcInvertedFile_la_SOURCES= \
	CAcIFFileSystem.cc\
        CAcIFMySQL.cc\
	\
        CAFIFMySQL.cc\
	CAFInvertedFile.cc\
	\
	CIFBuilderTriplet.cc\
	CDocumentFrequencyElement.cc \
	CDocumentFrequencyList.cc \
	\
	CIFListStart.cc \
	CInvertedFileChunk.cc \
	\
	CAdditionalDocumentInformation.cc\
	plug_in_fo.cc

# CLEANFILES=CAcIFFileSystem.cc
