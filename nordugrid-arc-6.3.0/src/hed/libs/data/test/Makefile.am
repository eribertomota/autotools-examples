TESTS = libarcdatatest
check_PROGRAMS = $(TESTS)

libarcdatatest_SOURCES = $(top_srcdir)/src/Test.cpp FileCacheTest.cpp
libarcdatatest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS)
libarcdatatest_LDADD = \
	$(top_builddir)/src/hed/libs/data/libarcdata.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS)
