#
# AutoMake
#
ACLOCAL_AMFLAGS = -I build
#
# Subdirectories to process
#
SUBDIRS = cf examples local sensible_mda
#
# Kluge to get my own targets include as recursive
#
RECURSIVE_TARGETS = build-arch-recursive build-indep-recursive \
       install-arch-recursive install-indep-recursive
#
# Debian targets, phase out
#
.PHONY: build-indep build-indep-am
.PHONY: build-arch  build-arch-am
.PHONY: install-indep install-indep-am
.PHONY: install-arch  install-arch-am
build-indep: build-indep-recursive
build-indep-am:
build-arch: build-arch-recursive
build-arch-am:
install-indep: install-indep-recursive
install-indep-am:
install-arch: install-arch-recursive
install-arch-am:
