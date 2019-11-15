TESTS = ChainTest

check_LTLIBRARIES = libtestmcc.la libtestservice.la
check_PROGRAMS = $(TESTS)

libtestmcc_la_SOURCES = TestMCC.cpp
libtestmcc_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libtestmcc_la_LIBADD = \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS)
libtestmcc_la_LDFLAGS = -no-undefined -avoid-version -module -rpath $(CURDIR)

libtestservice_la_SOURCES = TestService.cpp
libtestservice_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libtestservice_la_LIBADD = \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS)
libtestservice_la_LDFLAGS = -no-undefined -avoid-version -module -rpath $(CURDIR)

ChainTest_SOURCES = $(top_srcdir)/src/Test.cpp ChainTest.cpp
ChainTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
ChainTest_LDADD = \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS)
