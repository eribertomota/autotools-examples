SUBDIRS = schema

pkglib_LTLIBRARIES = libpythonservice.la

libpythonservice_la_SOURCES = pythonwrapper.cpp pythonwrapper.h
libpythonservice_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(PYTHON_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libpythonservice_la_LDFLAGS = -no-undefined -avoid-version -module
libpythonservice_la_LIBADD = \
	$(top_builddir)/src/hed/libs/infosys/libarcinfosys.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(PYTHON_LIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS) $(DLOPEN_LIBS)
