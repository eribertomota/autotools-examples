#try replacing with noinst_PROGRAMS
bin_PROGRAMS = ifpline

if WANT_EXAMPLES
  bin_PROGRAMS += simple
endif

check_PROGRAMS = selftest
TESTS = selftest

ifpline_SOURCES = ifpline.c
ifpline_LDADD = $(top_builddir)/src/libifp.la

#EXTRA_PROGRAMS = getfat

simple_SOURCES = simple.c
simple_LDADD = $(top_builddir)/src/libifp.la
#simple_LDADD = -L../src -lifp

selftest_SOURCES = selftest.c
selftest_LDADD = $(top_builddir)/src/libifp.la

#getfat_SOURCES = getfat.c
#getfat_LDADD = $(top_builddir)/src/libifp.la

# set the include path found by configure

INCLUDES = $(all_includes) -I$(top_srcdir)/include


