pkglib_LTLIBRARIES = libmodcrypto.la

libmodcrypto_la_SOURCES = crypto.cpp
libmodcrypto_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libmodcrypto_la_LIBADD = \
	$(top_builddir)/src/hed/libs/crypto/libarccrypto.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la
libmodcrypto_la_LDFLAGS = -no-undefined -avoid-version -module
