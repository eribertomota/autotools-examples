AM_CPPFLAGS = -DLOCALEDIR=\"$(datadir)/locale\" -DPREFIX=\"$(prefix)\"
AM_CFLAGS = -Wall $(GKDEBCONF_CFLAGS)

bin_PROGRAMS = gkdebconf

gkdebconf_LDADD = $(GKDEBCONF_LIBS)
gkdebconf_SOURCES = main.c files.c interface.c debconf.c cbs.c config.c
