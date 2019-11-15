TESTS = InformationInterfaceTest
check_PROGRAMS = $(TESTS)

InformationInterfaceTest_SOURCES = $(top_srcdir)/src/Test.cpp \
	InformationInterfaceTest.cpp
InformationInterfaceTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
InformationInterfaceTest_LDADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	../libarcinfosys.la $(CPPUNIT_LIBS) $(GLIBMM_LIBS)
