DIST_SUBDIRS = test
SUBDIRS = $(TEST_DIR)

noinst_LTLIBRARIES = libarcdelegation.la
#noinst_PROGRAMS = test

libarcdelegation_ladir = $(pkgincludedir)/delegation
libarcdelegation_la_HEADERS = DelegationInterface.h
libarcdelegation_la_SOURCES = DelegationInterface.cpp
libarcdelegation_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(AM_CXXFLAGS)
libarcdelegation_la_LIBADD = \
	$(top_builddir)/src/hed/libs/crypto/libarccrypto.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/ws-addressing/libarcwsaddressing.la \
	$(OPENSSL_LIBS)

#test_SOURCES = test.cpp
#test_CXXFLAGS = -I$(top_srcdir)/include \
#	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
#test_LDADD = libarcdelegation.la \
#	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
#	$(GLIBMM_LIBS) $(OPENSSL_LIBS)
