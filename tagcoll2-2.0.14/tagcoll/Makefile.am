## Process this file with automake to produce Makefile.in

SUBDIRS = tagexpr .

tagcollincludedir = $(includedir)/tagcoll-$(VERSION)/tagcoll
tagcollutilsincludedir = $(tagcollincludedir)/utils
tagcollinputincludedir = $(tagcollincludedir)/input
tagcolldiskindexincludedir = $(tagcollincludedir)/diskindex
tagcollstreamincludedir = $(tagcollincludedir)/stream
tagcollcollincludedir = $(tagcollincludedir)/coll

dist_tagcollutilsinclude_HEADERS = \
		utils/set.h

dist_tagcollinputinclude_HEADERS = \
		input/base.h \
		input/memory.h \
		input/string.h \
		input/stdio.h \
		input/zlib.h

dist_tagcolldiskindexinclude_HEADERS = \
		diskindex/mmap.h \
		diskindex/int.h \
		diskindex/string.h

dist_tagcollstreaminclude_HEADERS = \
		stream/sink.h \
		stream/filters.h \
		stream/filters.tcc \
		stream/expression.h \
		stream/substitutions.h \
		stream/patcher.h

dist_tagcollcollinclude_HEADERS = \
		coll/base.h \
		coll/base.tcc \
		coll/simple.h \
		coll/simple.tcc \
		coll/fast.h \
		coll/fast.tcc \
		coll/patched.h \
		coll/patched.tcc \
		coll/intdiskindex.h

dist_tagcollinclude_HEADERS = \
		expression.h \
		\
		patch.h \
		patch.tcc \
		\
		TextFormat.h \
		TextFormat.tcc \
		\
		Implications.h \
		Implications.tcc \
		DerivedTags.h \
		\
		SmartHierarchy.h \
		SmartHierarchy.tcc

# This library gets the non-template code
# (and currently some tests)
lib_LTLIBRARIES = libtagcoll2.la
libtagcoll2_la_SOURCES = \
		input/base.cc \
		input/memory.cc \
		input/string.cc \
		input/stdio.cc \
		input/zlib.cc \
		\
		diskindex/mmap.cc \
		diskindex/int.cc \
		diskindex/string.cc \
		\
		expression.cc \
		\
		coll/intdiskindex.cc \
		\
		SmartHierarchy.cc \
		TextFormat.cc

libtagcoll2_la_LIBADD = tagexpr/libtagexpr.la
libtagcoll2_la_LDFLAGS = $(LIBWIBBLE_LIBS) -version-info @LIBTAGCOLL_VERSION_INFO@

# Tests
TESTS_ENVIRONMENT = $(top_srcdir)/tagcoll/runtest
check_PROGRAMS = tests/libtagcoll-test

check-local:
	for test in $(check_PROGRAMS); do \
		$(TESTS_ENVIRONMENT) $$test ; \
	done

tests_libtagcoll_test_SOURCES = \
		stream/sink-tut.cc \
		stream/filters-tut.cc \
		stream/expression-tut.cc \
		stream/substitutions-tut.cc \
		stream/patcher-tut.cc \
		\
		diskindex/mmap-tut.cc \
		diskindex/int-tut.cc \
		diskindex/string-tut.cc \
		\
		coll/simple-tut.cc \
		coll/fast-tut.cc \
		coll/patched-tut.cc \
		coll/intdiskindex-tut.cc \
		\
		expression-tut.cc \
		TextFormat-tut.cc \
		patch-tut.cc \
		Implications-tut.cc \
		DerivedTags-tut.cc \
		SmartHierarchy-tut.cc \
		tests/tut-main.cpp
tests_libtagcoll_test_LDADD = libtagcoll2.la tagexpr/libtagexpr.la @LIBWIBBLE_LIBS@ -lz

DISTCLEANFILES = \
	tagcoll/tagexpr/Tagexpr_parser_y.hh \
	tagcoll/tagexpr/Tagexpr_parser_y.cc \
	tagcoll/tagexpr/Tagexpr_parser_l.cc

EXTRA_DIST = tests/test-utils.h tests/test-utils.tcc runtest

AM_CPPFLAGS = -I$(top_srcdir) $(LIBWIBBLE_DEFS)
