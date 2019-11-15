pkglib_LTLIBRARIES = libdmcs3.la

libdmcs3_la_SOURCES = DataPointS3.cpp DataPointS3.h 
libdmcs3_la_CXXFLAGS = -I$(top_srcdir)/include \
        $(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS) $(OPENSSL_CFLAGS) $(S3_CFLAGS)
libdmcs3_la_LIBADD = \
        $(top_builddir)/src/hed/libs/data/libarcdata.la \
        $(top_builddir)/src/hed/libs/message/libarcmessage.la \
        $(top_builddir)/src/hed/libs/loader/libarcloader.la \
        $(top_builddir)/src/hed/libs/common/libarccommon.la \
        $(LIBXML2_LIBS) $(GLIBMM_LIBS) $(OPENSSL_LIBS) $(S3_LIBS)
libdmcs3_la_LDFLAGS = -no-undefined -avoid-version -module
