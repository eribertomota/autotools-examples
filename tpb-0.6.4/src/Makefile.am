## Process this file with automake to produce Makefile.in

bin_PROGRAMS = tpb
tpb_SOURCES  = tpb.c cfg.c

localedir = $(datadir)/locale

INCLUDES = -I. -I$(srcdir) -I.. -I../intl
DEFS = @DEFS@ -DLOCALEDIR=\"$(localedir)\" -DSYSCONFDIR=\"@sysconfdir@\"

## Makefile.am ends here
