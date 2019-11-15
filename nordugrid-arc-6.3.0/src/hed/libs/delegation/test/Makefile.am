TESTS = DelegationInterfaceTest
check_PROGRAMS = $(TESTS)

DelegationInterfaceTest_SOURCES = $(top_srcdir)/src/Test.cpp \
	DelegationInterfaceTest.cpp
DelegationInterfaceTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
DelegationInterfaceTest_LDADD = \
	$(top_builddir)/src/hed/libs/delegation/libarcdelegation.la \
	$(CPPUNIT_LIBS)
