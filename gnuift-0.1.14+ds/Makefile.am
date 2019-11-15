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

#gift-config.cc: gift-config.cc.in make-gift-config.pl
#	perl make-gift-config.pl CXXFLAGS "$(CXXFLAGS)" LDFLAGS "$(LDFLAGS)" libdir "-l $(libdir)" < $< > $@

SUBDIRS=  Doc scripts dtd \
	@UNPUBLISHED_DIR@ \
	libMRML \
	libGIFTAcURL2FTS\
	libGIFTAcHierarchy libGIFTQuHierarchy\
	libGIFTAcInvertedFile libGIFTQuInvertedFile\
	libGIFTAcPerl libGIFTQuPerl \
	libGIFTAcDistanceMatrix\
        @GIFT_BAYESIAN_DIR@ libSquirePPM GIFTServer FeatureExtraction 


# doc should be the choice of the user...
# libGIFTAcDistanceMatrix needs some unpublished class
# where I (WM) have to look on to do accessor/query engine
# separation
# EXTRA_SUBDIRS=	Doc



EXTRA_DIST=PluginMaker \
		bootstrap-cvs.sh \
		notice.am \
		notice.c\
		notice.cc\
		notice.el\
		notice.h\
		notice.in\
		notice.java\
		notice.pre-pl\
		notice.pre-pm\
		perl-compile-test-program.cc\
		pthread-compile-test-program.cc\
		renamer.pl\
		gift-file-to-gift-file.pl      \
		gift-install-prerequisites.pl  \
		teco.sh\
		gift-install-prerequisites.sh\
		gift-check-perl-config.pl \
		aclocal-add.m4


