#
# NASPRO - The NASPRO Architecture for Sound PROcessing
# A collection of bridges to LV2
#
# Copyright (C) 2007-2014 Stefano D'Angelo
#
# See the COPYING file for license conditions.
#

if BUILD_LADSPA

AM_CFLAGS = -pedantic -Wall -Werror -Wno-strict-aliasing @NABRIT_CFLAGS@
AM_LDFLAGS = -no-undefined -module -avoid-version -shared @NABRIT_LIBS@

ladspadir = @lv2dir@/naspro-ladspa.lv2
ladspa_LTLIBRARIES = ladspa.la
ladspa_la_SOURCES = internal.h manifest.c bridge.h bridge.c pluglib.h \
		    pluglib.c plugin.h plugin.c lv2api.h lv2api.c

ladspa_DATA = manifest.ttl

# Hack to avoid having *.la files around
install-data-hook:
	rm -f $(DESTDIR)$(ladspadir)/ladspa.la

if INSTALL_LRDF
SUBDIRS = data
endif

endif
