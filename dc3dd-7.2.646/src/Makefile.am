bin_PROGRAMS = dc3dd

noinst_HEADERS = system.h 

if COND_USE_HDPARM
dc3dd_SOURCES = dc3dd.c hdparm/hpa_dco.c hdparm/identify.c hdparm/sgio.c
else
dc3dd_SOURCES = dc3dd.c
endif

AM_CPPFLAGS = -I$(top_srcdir)/lib

# Sometimes, the expansion of $(LIBINTL) includes -lc which may
# include modules defining variables like `optind', so libcoreutils.a
# must precede $(LIBINTL) in order to ensure we use GNU getopt.
# But libcoreutils.a must also follow $(LIBINTL), since libintl uses
# replacement functions defined in libcoreutils.a.
# TODO: is this the right place for -lpthread?
LDADD = ../lib/libcoreutils.a $(LIBINTL) ../lib/libcoreutils.a -lpthread

dc3dd_LDADD = $(LDADD) $(LIB_GETHRXTIME) $(LIB_FDATASYNC)
