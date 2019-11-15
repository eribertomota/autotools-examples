lib_LTLIBRARIES = libgrail.la
version_script = $(srcdir)/libgrail.ver

AM_CPPFLAGS = -DBUILDING_GRAIL $(WARNING_CPPFLAGS)

AM_CFLAGS = $(COVERAGE_CFLAGS) $(VISIBILITY_CFLAGS)

AM_CXXFLAGS = $(CXX11_CXXFLAGS) $(COVERAGE_CXXFLAGS) $(VISIBILITY_CXXFLAGS)

libgrail_la_LDFLAGS = \
	-version-info @LIB_VERSION@ \
	-Wl,--version-script=$(version_script)

libgrail_la_LIBADD = \
	$(FRAME_LIBS) \
	$(COVERAGE_LIBS) \
	-lm

libgrail_la_SOURCES = \
	atomic-recognizer.cpp \
	atomic-recognizer.h \
	event.cpp \
	event.h \
	forward.h \
	gesture.cpp \
	gesture.h \
	handle.cpp \
	handle.h \
	log.cpp \
	log.h \
	recognizer.cpp \
	recognizer.h \
	regular-recognizer.cpp \
	regular-recognizer.h \
	slice.cpp \
	slice.h \
	subscription.cpp \
	subscription.h \
	touch.cpp \
	touch.h

INCLUDES = -I$(top_srcdir)/include/ $(FRAME_CFLAGS)

libgrail_includedir = $(includedir)/oif
libgrail_include_HEADERS = \
	$(top_srcdir)/include/oif/grail.h

EXTRA_DIST = $(version_script)

