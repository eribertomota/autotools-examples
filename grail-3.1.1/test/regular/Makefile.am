test_targets = test-c-compile test-cxx-compile

if HAVE_GTEST
test_targets += check-regular
endif

TESTS = $(test_targets) 
check_PROGRAMS = $(test_targets)

test_c_compile_SOURCES = test-c-compile.c
test_c_compile_LDADD = \
	$(top_builddir)/src/libgrail.la \
	$(FRAME_LIBS)
test_c_compile_CFLAGS = \
	-I$(top_srcdir)/include \
	$(FRAME_CFLAGS)

test_cxx_compile_SOURCES = test-cxx-compile.cpp
test_cxx_compile_LDADD = \
	$(top_builddir)/src/libgrail.la \
	$(FRAME_LIBS)
test_cxx_compile_CPPFLAGS = \
	-I$(top_srcdir)/include \
	$(FRAME_CFLAGS)

check_regular_SOURCES = \
	grail.cpp \
	grail-fixture.cpp \
	grail-fixture.h \
	intermittent_3touch.cpp \
	one-touch-gest-finished.cpp \
	pending-end.cpp \
	still-gest-finishes.cpp \
	subscription.cpp

#
# Link against the (non-distributed) static lib to pick up the
# internal symbols.
#
check_regular_LDADD = \
	$(top_builddir)/src/.libs/libgrail.a \
	$(top_builddir)/test/gtest/libgtest_grail.a \
	$(COVERAGE_LIBS) \
	$(GTEST_LIBS) \
	$(FRAME_LIBS)

check_regular_CPPFLAGS = \
	--std=c++0x \
	-I$(top_srcdir) \
	-I$(top_srcdir)/include \
	$(WARNING_CPPFLAGS) \
	$(GTEST_CPPFLAGS) \
	$(FRAME_CFLAGS)

check_regular_CFLAGS = \
	$(COVERAGE_CFLAGS)

