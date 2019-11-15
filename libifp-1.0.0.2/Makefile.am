
# not a GNU package. You can remove this line, if
# have all needed files, that a GNU package needs
AUTOMAKE_OPTIONS = foreign 1.4
INCLUDES = -I$(top_srcdir)/include
#SUBDIRS = src examples
EXTRA_DIST = src/ifp_os.h  src/prim.h  src/ifp_os_linux.c src/main.c docs/man/man3/ifp.h.3 docs/doxygen.in  dpkg/Makefile.in docs/Makefile.in kbuild/Makefile.in
man3_MANS = docs/man/man3/ifp.h.3

if WANT_USERLAND
MAYBE_USERLAND = src examples
endif
if COND_KBUILD
MAYBE_KBUILD = kbuild
endif

SUBDIRS = $(MAYBE_USERLAND) $(MAYBE_KBUILD)

libtool: $(LIBTOOL_DEPS)
	$(SHELL) ./config.status --recheck

docs:
	cd docs; make

deb: dist
	cd dpkg; make

test: check

.PHONY: docs deb test

