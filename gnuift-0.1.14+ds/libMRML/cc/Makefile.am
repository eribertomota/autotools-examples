#     -*- Mode: makefile -*-

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

CCCONFIG=sed -e "s:__EXECBINDIR__:@DEBEXECBINDIR@:g;s:__PERL_LOCATION__:@PERL@:g;s:__BINDIR__:@DEBPERLLIBDIR@:g;s:__DATADIR__:@DEBDATADIR@:g;s:__LIBDIR__:@DEBSHAREDIR@:g;s:__HOME__:${HOME}:g;s:__WEB_PUBLISHING_DIRECTORY__:@WEB_PUBLISHING_DIRECTORY@:g;s§__WEB_PUBLISHING_LOCATION__§@WEB_PUBLISHING_LOCATION@§g;" < $< > $@

# noinst_LIBRARIES= libMRML.a

lib_LTLIBRARIES = libMRML.la

INCLUDES= -DHAS_BOOL \
	-DLINK_DYNAMICALLY\
	-I$(top_srcdir)

libMRML_la_LDFLAGS=@PRE_INSTALL_LIBDIRS@  -version-info 4:0:3

#CAccessorAdminCollection.cc: CAccessorAdminCollection.pre-cc
#	$(CCCONFIG)

# libMRML_a_SOURCES= 



libMRML_la_SOURCES= \
	 getLibNameFromFileName.cc\
	\
	CAccessorElement.cc\
	\
	CAccessor.cc\
	CAccessorImplementation.cc\
	\
	CAccessorFactoryContainer.cc\
	CAccessorFactory.cc\
	CAFPlugin.cc\
	\
	CRelevanceLevel.cc \
	CRelevanceLevelList.cc \
	\
	CIDRelevanceLevelPair.cc \
	CIDRelevanceLevelPairList.cc \
	\
	CAccessorAdmin.cc \
	CAccessorAdminCollection.cc \
	CPropertySheetList.cc \
	CSessionManager.cc \
	\
	CAlgorithmCollection.cc \
	\
	CDynamicQueryFactory.cc\
	CQueryPlugin.cc\
	CStaticQueryFactory.cc\
	\
	GIFTExceptions.cc \
	\
	CAttributeList.cc \
	CXMLHelper.cc \
	CXMLElement.cc \
	\
	CAlgorithm.cc \
	\
	CQueryTreeNode.cc\
	CQueryTreeBuilder.cc\
	\
	CQuery.cc \
	CQMultiple.cc \
	\
	CMagic.cc\
	\
	CQueryParadigmMatcher.cc\
	\
	mrml_const.cc\
	\
	CXMLElementVisitor.cc\
	CXMLElementBuilder.cc\
	CXEVCommunication.cc\
	\
	CMutex.cc\
	\
	CCommunicationHandler.cc\
	\
	CTimeStampGenerator.cc\
	\
	CDebuggingMemoryManager.cc\
	CRPipe.cc CReaper.cc CReaperDistributor.cc safePopen.cc\
	createErrorMessage.cc\
	CI18nTranslator.cc 	CXEVI18nTranslator.cc

CLEANFILES=libMRML-config.cc

#libMRML-config.cc: libMRML-config.pre-cc ../../make-gift-config.pl
#	perl ../../make-gift-config.pl CXXFLAGS ' $(CXXFLAGS) ' INCLUDES ' -I$(includedir)/libMRML/include ' LDFLAGS '$(LDFLAGS)' LIBS ' $(LIBS) ' libdir ' -L $(libdir) '  < libMRML-config.pre-cc  > libMRML-config.cc
libMRML-config.cc: libMRML-config.pre-cc
	sed -e "s§%CXXFLAGS%§$(CXXFLAGS) -I$(includedir)§g;\
	        s§%INCLUDES%§-I$(includedir)§g;\
                s§%LDFLAGS%§$(LDFLAGS)§g;\
                s§%LIBS%§$(LIBS)§ g;\
                s§%GIFT_MYSQL_DIR%§@GIFT_MYSQL_DIR@§g;\
	        s§%libdir%§$(libdir)§g;"  < libMRML-config.pre-cc  > libMRML-config.cc

bin_PROGRAMS= libMRML-config

libMRML_config_SOURCES= libMRML-config.cc 

EXTRA_DIST=libMRML-config.pre-cc

dist-hook:
	rm $(distdir)/libMRML-config.cc
