CPPFLAGS = @CPPFLAGS@ $(shell dpkg-buildflags --get CPPFLAGS)
sbin_PROGRAMS = sensible-mda
#
# Shipped manpages
#
dist_man_MANS = sensible-mda.8
#
# Program sources
#
sensible_mda_SOURCES = sensible-mda.c
#
# Debian targets, phase out
#
.PHONY: build-indep build-arch
.PHONY: install-indep install-arch
build-indep:
build-arch: sensible-mda
install-indep:
install-arch: install
