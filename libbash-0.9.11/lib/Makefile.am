AUTOMAKE_OPTIONS = -Wno-portability

EXTRA_DIST = $(wildcard *.sh) $(wildcard *.man)

# all libraries goes to lib/bash

bashlibdir = $(libdir)/bash
bashlib_DATA = $(wildcard *.sh)

# installing man pages
#######################

# getopts is treated specially since we install man pages in different sections
man3_MANS =	getopts.man
man1_MANS =	getopt_long.man

BASHLIBS = hashstash colors messages locks urlcoding

# The macro finds all man page files that reference $(1) in section $(2)
define GET_MANS
$(shell grep '^\.so man$(2)/$(1).$(2)$$' * |cut -f1 -d:)
endef

# note the `+'
$(foreach lib,$(BASHLIBS),$(eval man3_MANS+=$(lib).man $(call GET_MANS,$(lib),3)))

