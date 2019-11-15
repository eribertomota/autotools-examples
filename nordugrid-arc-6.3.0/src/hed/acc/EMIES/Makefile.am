SUBDIRS = schema

pkglib_LTLIBRARIES = libaccEMIES.la
bin_PROGRAMS = arcemiestest
man_MANS = arcemiestest.1

libaccEMIES_la_SOURCES  = EMIESClient.cpp EMIESClient.h \
	JobStateEMIES.cpp JobStateEMIES.h \
	SubmitterPluginEMIES.cpp SubmitterPluginEMIES.h \
	JobControllerPluginEMIES.cpp JobControllerPluginEMIES.h \
	JobListRetrieverPluginEMIES.cpp JobListRetrieverPluginEMIES.h \
	TargetInformationRetrieverPluginEMIES.cpp TargetInformationRetrieverPluginEMIES.h \
	DescriptorsEMIES.cpp
libaccEMIES_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS)
libaccEMIES_la_LIBADD = \
	$(top_builddir)/src/hed/libs/delegation/libarcdelegation.la \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/communication/libarccommunication.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la\
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS) $(GLIBMM_LIBS)
libaccEMIES_la_LDFLAGS = -no-undefined -avoid-version -module

#	$(top_builddir)/src/hed/libs/security/libarcsecurity.la \
#	$(top_builddir)/src/hed/libs/data/libarcdata.la \
#	$(top_builddir)/src/hed/libs/ws/libarcws.la \
#	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
#

arcemiestest_SOURCES = TestEMIESClient.cpp EMIESClient.cpp JobStateEMIES.cpp
arcemiestest_CXXFLAGS = -I$(top_srcdir)/include $(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS)
arcemiestest_LDADD = \
	$(top_builddir)/src/hed/libs/delegation/libarcdelegation.la \
	$(top_builddir)/src/hed/libs/communication/libarccommunication.la \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS) $(GLIBMM_LIBS)

#DIST_SUBDIRS = test
#SUBDIRS = $(TEST_DIR)
