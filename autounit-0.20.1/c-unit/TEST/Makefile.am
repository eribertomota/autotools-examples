OUR_UNIT_TESTS = test-au-netstring test-suite test-test

TESTS = $(OUR_UNIT_TESTS)

check_PROGRAMS = $(OUR_UNIT_TESTS)

test_au_netstring_SOURCES = test-au-netstring.c
test_au_netstring_LDADD = ../libau-c-unit.la $(GLIB_LIBS)
test_au_netstring_CFLAGS = $(GLIB_CFLAGS) -I..

test_test_SOURCES = test-test.c
test_test_LDADD = ../libau-c-unit.la $(GLIB_LIBS)
test_test_CFLAGS = $(GLIB_CFLAGS) -I..

test_suite_SOURCES = test-suite.c
test_suite_LDADD = ../libau-c-unit.la $(GLIB_LIBS)
test_suite_CFLAGS = $(GLIB_CFLAGS) -I..

AM_CFLAGS = -I$(top_srcdir)/c-unit -I.. -I$(top_srcdir) -I../..
