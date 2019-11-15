pkglib_LTLIBRARIES = libaccBroker.la

libaccBroker_la_SOURCES = \
	FastestQueueBrokerPlugin.cpp FastestQueueBrokerPlugin.h \
	RandomBrokerPlugin.h \
	DescriptorsBroker.cpp \
	BenchmarkBrokerPlugin.cpp BenchmarkBrokerPlugin.h \
	DataBrokerPlugin.cpp DataBrokerPlugin.h \
	NullBrokerPlugin.h
libaccBroker_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS)
libaccBroker_la_LIBADD = \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/communication/libarccommunication.la \
	$(top_builddir)/src/hed/libs/data/libarcdata.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS) $(GLIBMM_LIBS)
libaccBroker_la_LDFLAGS  = -no-undefined -avoid-version -module

DIST_SUBDIRS = test
SUBDIRS = $(TEST_DIR)
