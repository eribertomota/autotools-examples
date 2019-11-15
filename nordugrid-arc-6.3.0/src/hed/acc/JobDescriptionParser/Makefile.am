pkglib_LTLIBRARIES = libaccJobDescriptionParser.la

libaccJobDescriptionParser_la_SOURCES = \
	ADLParser.cpp ADLParser.h \
	XRSLParser.cpp XRSLParser.h \
	RSLParser.cpp RSLParser.h \
	XMLNodeRecover.cpp XMLNodeRecover.h \
	DescriptorsJobDescriptionParser.cpp
libaccJobDescriptionParser_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS)
libaccJobDescriptionParser_la_LIBADD = \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS) $(GLIBMM_LIBS)
libaccJobDescriptionParser_la_LDFLAGS = -no-undefined -avoid-version -module

DIST_SUBDIRS = test
SUBDIRS = $(TEST_DIR)
