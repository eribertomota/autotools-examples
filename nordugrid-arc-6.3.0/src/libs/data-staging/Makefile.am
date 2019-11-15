DIST_SUBDIRS = test examples
SUBDIRS = . $(TEST_DIR) examples

lib_LTLIBRARIES = libarcdatastaging.la

libarcdatastaging_ladir = $(pkgincludedir)/data-staging

libarcdatastaging_la_HEADERS = DataDelivery.h DataDeliveryComm.h \
  DataDeliveryLocalComm.h DataDeliveryRemoteComm.h DTR.h DTRList.h \
  DTRStatus.h Processor.h Scheduler.h TransferShares.h

libarcdatastaging_la_SOURCES = DataDelivery.cpp DataDeliveryComm.cpp \
  DataDeliveryLocalComm.cpp DataDeliveryRemoteComm.cpp DTR.cpp DTRList.cpp \
  DTRStatus.cpp Processor.cpp Scheduler.cpp TransferShares.cpp

libarcdatastaging_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(AM_CXXFLAGS)
libarcdatastaging_la_LIBADD = \
  $(top_builddir)/src/hed/libs/common/libarccommon.la \
  $(top_builddir)/src/hed/libs/data/libarcdata.la \
  $(top_builddir)/src/hed/libs/message/libarcmessage.la \
  $(top_builddir)/src/hed/libs/loader/libarcloader.la \
  $(top_builddir)/src/hed/libs/communication/libarccommunication.la \
  $(GLIBMM_LIBS)
libarcdatastaging_la_LDFLAGS = -version-info 3:0:0

pgmpkglibdir = $(pkglibdir)
pgmpkglib_PROGRAMS = DataStagingDelivery

DataStagingDelivery_SOURCES = DataStagingDelivery.cpp
DataStagingDelivery_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(AM_CXXFLAGS)
DataStagingDelivery_LDADD = \
	$(top_builddir)/src/hed/libs/data/libarcdata.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(GLIBMM_LIBS)
