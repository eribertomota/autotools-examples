lib_LTLIBRARIES = libarccrypto.la

libarccrypto_ladir = $(pkgincludedir)/crypto
libarccrypto_la_HEADERS = OpenSSL.h
libarccrypto_la_SOURCES = OpenSSL.cpp
libarccrypto_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(OPENSSL_CFLAGS) $(AM_CXXFLAGS)
libarccrypto_la_LIBADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(GLIBMM_LIBS) $(GTHREAD_LIBS) $(OPENSSL_LIBS)
libarccrypto_la_LDFLAGS = -version-info 3:0:0
