# Include flags for the compile phrase. 
# Variables are from configure.in in the top directory.
INCLUDES = -I$(top_srcdir) -I$(includedir) \
    -DG_LOG_DOMAIN=\"yyt\" \
    -I../intl -I$(top_srcdir)/intl


# list the programs to be compiled.
bin_PROGRAMS = yyt

# list the files to be compiled to create the programs listed in the
# bin_PROGRAMS. (e.g. holytalk -> holytalk_SOURCES) Files here will be 
# included in the distrubtions.
yyt_SOURCES = \
    xmalloc.c common.h\
    cmdline.c cmdline.h \
    hzsegment.c hzsegment.h \
    loop.c loop.h \
    parseinput.c parseinput.h \
    setty.c setty.h \
    yiyantang.c yiyantang.h \
    yiyantang_init.c yiyantang_init.h \
    yyt_util.c yyt_util.h \
    zhconv.c zhconv.h \
    zhinit.c zhinit.h

# Library flags for the link phrase. Variables are from configure.in
# preffix are determined by bin_PROGRAMS.
yyt_LDADD = $(LIBOBJS) $(INTLLIBS)
yyt_DEPENDENCIES = $(LIBOBJS)
EXTRA_yyt_SOURCES = getopt.h

check_PROGRAMS = test-hzsegment
test_hzsegment_SOURCES = test_hzsegment.c \
			 hzsegment.c hzsegment.h

%.c: %.ggo
	gengetopt --input=$< --long-help -u

EXTRA_DIST = cmdline.ggo

# We should have targets as: dist, distcheck, clean, install,
#	uninstall, distclean, mostlyclean, maintainer-clean,
#	TAGS, check.
