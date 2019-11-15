pkglib_LTLIBRARIES = libdatadeliveryservice.la

if SYSV_SCRIPTS_ENABLED
DATA_DELIVERY_SCRIPT = arc-datadelivery-service
else
DATA_DELIVERY_SCRIPT =
endif
initd_SCRIPTS = $(DATA_DELIVERY_SCRIPT)

if SYSTEMD_UNITS_ENABLED
DATA_DELIVERY_UNIT = arc-datadelivery-service.service
else
DATA_DELIVERY_UNIT =
endif
units_DATA = $(DATA_DELIVERY_UNIT)

pkgdata_SCRIPTS = arc-datadelivery-service-start

libdatadeliveryservice_la_SOURCES = DataDeliveryService.h DataDeliveryService.cpp
libdatadeliveryservice_la_CXXFLAGS = -I$(top_srcdir)/include \
  $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libdatadeliveryservice_la_LIBADD = \
  $(top_builddir)/src/libs/data-staging/libarcdatastaging.la \
  $(top_builddir)/src/hed/libs/infosys/libarcinfosys.la \
  $(top_builddir)/src/hed/libs/message/libarcmessage.la \
  $(top_builddir)/src/hed/libs/loader/libarcloader.la \
  $(top_builddir)/src/hed/libs/common/libarccommon.la \
  $(top_builddir)/src/hed/libs/delegation/libarcdelegation.la \
  $(top_builddir)/src/hed/libs/data/libarcdata.la \
  $(GLIBMM_LIBS)
libdatadeliveryservice_la_LDFLAGS = -no-undefined -avoid-version -module
