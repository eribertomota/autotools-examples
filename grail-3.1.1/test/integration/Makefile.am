test_targets = check-integration

TESTS = $(test_targets) 
check_PROGRAMS = $(test_targets)

check_integration_SOURCES = \
	device.cpp \
	device.h \
	events.h \
	recording.cpp \
	recording.h \
	slice-checker.cpp \
	slice-checker.h \
	x11/fixture.cpp \
	x11/fixture.h \
	x11/no-premature-gestures.cpp \
	x11/no-tap-after-drag.cpp \
	x11/twodrag.cpp \
	x11/dragthresh.cpp \
	x11/timeout.cpp \
	x11/atomic-timeout.cpp \
	x11/tap-touch-accept.cpp \
	x11/parallel-atomic-gestures.cpp \
	x11/hold-reject.cpp

nodist_check_integration_SOURCES = \
	$(XORG_GTEST_SOURCE)/src/xorg-gtest_main.cpp

check_integration_CPPFLAGS = \
	--std=c++0x \
	-I$(top_srcdir) \
	-I$(top_srcdir)/include \
	-I../include \
	-DTEST_ROOT_DIR=\"$(abs_top_srcdir)/test/integration/\"\
	$(WARNING_CPPFLAGS) \
	$(GTEST_CPPFLAGS) \
	$(XORG_GTEST_CPPFLAGS)

check_integration_CFLAGS = \
	$(COVERAGE_CFLAGS) \
	$(FRAME_CFLAGS) \
	$(XORG_GTEST_CFLAGS)

check_integration_CXXFLAGS = \
	$(CXX11_CXXFLAGS) \
	$(COVERAGE_CXXFLAGS) \
	$(GTEST_CXXFLAGS) \
	$(XORG_GTEST_CXXFLAGS) \
	$(FRAME_CFLAGS)

#
# Link against the (non-distributed) static lib to pick up the
# internal symbols.
#
check_integration_LDADD = \
	$(top_builddir)/src/libgrail.la \
	$(top_builddir)/test/gtest/libgtest_grail.a \
	$(EVEMU_LIBS) \
	$(FRAME_LIBS) \
	$(COVERAGE_LIBS) \
	$(GTEST_LIBS) \
	$(XORG_GTEST_LIBS) \
	$(XINPUT_LIBS) \
	$(X11_LIBS)

EXTRA_DIST = io recordings
