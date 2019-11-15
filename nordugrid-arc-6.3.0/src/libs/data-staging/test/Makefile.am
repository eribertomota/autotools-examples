# Tests require mock DMC which can be enabled via configure --enable-mock-dmc
if MOCK_DMC_ENABLED
TESTS = DTRTest ProcessorTest DeliveryTest
else
TESTS =
endif
check_PROGRAMS = $(TESTS)

TESTS_ENVIRONMENT = env ARC_PLUGIN_PATH=$(top_builddir)/src/hed/dmc/mock/.libs:$(top_builddir)/src/hed/dmc/file/.libs

DTRTest_SOURCES = $(top_srcdir)/src/Test.cpp DTRTest.cpp
DTRTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
DTRTest_LDADD = ../libarcdatastaging.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(top_builddir)/src/hed/libs/credential/libarccredential.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS)

ProcessorTest_SOURCES = $(top_srcdir)/src/Test.cpp ProcessorTest.cpp
ProcessorTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
ProcessorTest_LDADD = ../libarcdatastaging.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(top_builddir)/src/hed/libs/credential/libarccredential.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS)

DeliveryTest_SOURCES = $(top_srcdir)/src/Test.cpp DeliveryTest.cpp
DeliveryTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
DeliveryTest_LDADD = ../libarcdatastaging.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(top_builddir)/src/hed/libs/credential/libarccredential.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS)

