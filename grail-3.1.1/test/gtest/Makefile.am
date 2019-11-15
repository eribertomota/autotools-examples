if HAVE_GTEST
  check_LIBRARIES = libgtest_grail.a
endif

nodist_libgtest_grail_a_SOURCES = \
	$(GTEST_SOURCE)/gtest-all.cc \
	$(GTEST_SOURCE)/gtest_main.cc

libgtest_grail_a_CPPFLAGS = \
	$(GTEST_CPPFLAGS)

if ENABLE_INTEGRATION_TESTS
nodist_libgtest_grail_a_SOURCES += \
	$(XORG_GTEST_SOURCE)/src/xorg-gtest-all.cpp

libgtest_grail_a_CPPFLAGS += \
	--std=c++0x \
	$(XORG_GTEST_CPPFLAGS) \
	$(XORG_GTEST_CFLAGS)
endif
