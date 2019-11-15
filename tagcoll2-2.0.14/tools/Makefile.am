## Process this file with automake to produce Makefile.in

TESTS = tagcoll-test

bin_PROGRAMS = tagcoll
# tagidx

tagcoll_SOURCES = tagcoll.cc
tagcoll_LDADD = ../tagcoll/libtagcoll2.la ../tagcoll/tagexpr/libtagexpr.la @LIBWIBBLE_LIBS@

AM_CPPFLAGS = -I$(top_srcdir)

EXTRA_DIST = TagcollParser.h Timing.h tagcoll-test \
	test-data/test-changes \
	test-data/test-collection \
	test-data/test-collection-colorsonly \
	test-data/test-collection-diffed \
	test-data/test-collection-faceted \
	test-data/test-collection-grepped \
	test-data/test-collection-items \
	test-data/test-collection-reversed \
	test-data/test-derived-tags \
	test-data/test-implications \
	test-data/test-parser-input \
	test-data/test-parser-input1 \
	test-data/test-patches
