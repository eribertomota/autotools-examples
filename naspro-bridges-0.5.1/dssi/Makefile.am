#
# NASPRO - The NASPRO Architecture for Sound PROcessing
# A collection of bridges to LV2
#
# Copyright (C) 2007-2014 Stefano D'Angelo
#
# See the COPYING file for license conditions.
#

if BUILD_DSSI

AM_CFLAGS = -pedantic -Wall -Werror -Wno-strict-aliasing \
	    @NABRIT_CFLAGS@ @DSSI_CFLAGS@ @ALSA_CFLAGS@
AM_LDFLAGS = -no-undefined -module -avoid-version -shared \
	     @NABRIT_LIBS@ @ALSA_LIBS@

dssidir = @lv2dir@/naspro-dssi.lv2
dssi_LTLIBRARIES = dssi.la
dssi_la_SOURCES = internal.h manifest.c bridge.h bridge.c pluglib.h pluglib.c \
		  plugin.h plugin.c lv2api.h lv2api.c

dssi_DATA = manifest.ttl

# Hack to avoid having *.la files around
install-data-hook:
	rm -f $(DESTDIR)$(dssidir)/dssi.la

endif
