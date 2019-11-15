pkglib_LTLIBRARIES = libaccPythonBroker.la

libaccPythonBroker_la_SOURCES = PythonBrokerPlugin.cpp PythonBrokerPlugin.h
libaccPythonBroker_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(PYTHON_CFLAGS) $(AM_CXXFLAGS)
libaccPythonBroker_la_LIBADD = \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(GLIBMM_LIBS) $(LIBXML2_LIBS) $(PYTHON_LIBS)
libaccPythonBroker_la_LDFLAGS = -no-undefined -avoid-version -module

exampledir = $(pkgdatadir)/examples/PythonBroker
example_DATA = SampleBroker.py ACIXBroker.py

EXTRA_DIST = $(example_DATA)
