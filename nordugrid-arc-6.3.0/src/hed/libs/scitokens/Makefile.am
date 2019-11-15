#DIST_SUBDIRS = test
#SUBDIRS = $(TEST_DIR)

lib_LTLIBRARIES = libarcscitokens.la

pgmpkglibdir = $(pkglibdir)
pgmpkglib_PROGRAMS =

libarcscitokens_ladir = $(pkgincludedir)
libarcscitokens_la_HEADERS = jwse.h
libarcscitokens_la_SOURCES = jwse.cpp jwse_hmac.cpp jwse_ecdsa.cpp jwse_keys.cpp
libarcscitokens_la_CXXFLAGS = -I$(top_srcdir)/include $(OPENSSL_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS)
libarcscitokens_la_LIBADD = \
        $(top_builddir)/src/external/cJSON/libcjson.la \
        $(top_builddir)/src/hed/libs/common/libarccommon.la \
        $(OPENSSL_LIBS) $(GLIBMM_LIBS) $(LIBINTL)
libarcscitokens_la_LDFLAGS = -version-info 3:0:0
