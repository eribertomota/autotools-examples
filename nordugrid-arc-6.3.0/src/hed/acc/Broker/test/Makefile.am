TESTS = BenchmarkBrokerTest
check_PROGRAMS = $(TESTS)

BenchmarkBrokerTest_SOURCES = $(top_srcdir)/src/Test.cpp \
	BenchmarkBrokerTest.cpp
BenchmarkBrokerTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
BenchmarkBrokerTest_LDADD = \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
        $(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS)
