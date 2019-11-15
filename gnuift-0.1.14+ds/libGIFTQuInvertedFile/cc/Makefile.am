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

lib_LTLIBRARIES = libGIFTQuInvertedFile.la

libGIFTQuInvertedFile_la_LDFLAGS="@PRE_INSTALL_LIBDIRS@"  -lMRML -lGIFTAcInvertedFile

#
# The trick here is: do not compile c code with the -D bool=char define.
#-rdynamic
INCLUDES= -DHAS_BOOL -I$(top_srcdir)/libMRML/include -I$(top_srcdir)/libGIFTQuInvertedFile/include -I$(top_srcdir)/libGIFTAcInvertedFile/include 

libGIFTQuInvertedFile_la_SOURCES= \
	CWeightingFunction.cc \
	CWFBestFullyWeighted.cc \
	CWFBestProbabilistic.cc \
	CWFClassicalIDF.cc \
	CWFBinaryTerm.cc \
	CWFStandardTF.cc \
	CWFCoordinationLevel.cc \
	CWFProbability.cc \
	\
	CWeighter.cc\
	\
	CWeightingFunctionPointerHash.cc \
	CScoreBoard.cc \
	\
	CQueryNormalizer.cc \
	CQNNoNormalization.cc \
	CQNMaxDocumentFrequency.cc \
	CQNEuclideanLengthSquare.cc \
	CQNSquareDFLogICFSum.cc \
	\
	CQInvertedFile.cc \
	plug_in_fo.cc