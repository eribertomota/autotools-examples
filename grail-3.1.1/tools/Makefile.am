dist_man_MANS = \
	grail-test-3-1.1 \
	grail-test-atomic.1 \
	grail-test-edge.1 \
	grail-test-propagation.1

bin_PROGRAMS = \
	grail-test-propagation \
	grail-test-edge \
	grail-test-3-1 \
	grail-test-atomic

grail_test_propagation_SOURCES = grail-test-propagation.c \
	common/device.c \
	common/device.h \
	common/servertime.c \
	common/servertime.h \
	common/slice.c \
	common/slice.h

grail_test_edge_SOURCES = grail-test-edge.c \
	common/device.c \
	common/device.h \
	common/servertime.c \
	common/servertime.h \
	common/slice.c \
	common/slice.h

grail_test_3_1_SOURCES = grail-test-3-1.c \
	common/device.c \
	common/device.h \
	common/servertime.c \
	common/servertime.h \
	common/slice.c \
	common/slice.h

grail_test_atomic_SOURCES = grail-test-atomic.c \
	common/device.c \
	common/device.h \
	common/servertime.c \
	common/servertime.h \
	common/slice.c \
	common/slice.h

INCLUDES=-I$(top_srcdir)/include/

AM_CPPFLAGS = $(WARNING_CPPFLAGS)

AM_CFLAGS = $(X11_CFLAGS) $(XINPUT_CFLAGS) $(FRAME_CFLAGS) $(COVERAGE_CFLAGS)

LDADD = \
	$(top_builddir)/src/libgrail.la \
	$(FRAME_LIBS) \
	$(X11_LIBS) \
	$(XINPUT_LIBS) \
	$(COVERAGE_LIBS) \
	-lm
