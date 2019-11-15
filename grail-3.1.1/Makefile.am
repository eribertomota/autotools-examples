ACLOCAL_AMFLAGS = -I m4 --install
AM_DISTCHECK_CONFIGURE_FLAGS = --disable-integration-tests

SUBDIRS = src test

# all tools are X11-specific
if HAVE_XINPUT
SUBDIRS += tools
endif

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = grail.pc

INCLUDES = $(top_srcdir)/include/

if HAVE_GCOV
  .PHONY: coverage-html generate-coverage-html coverage-html-clean
  coverage-html:
	-$(MAKE) $(AM_MAKEFLAGS) -k check
	$(MAKE) $(AM_MAKEFLAGS) generate-coverage-html

  generate-coverage-html:
	@echo Collecting coverage data
	$(LCOV) --directory $(top_builddir) --base-directory src --capture --output-file coverage.info --no-checksum --compat-libtool
	LANG=C $(GENHTML) --prefix $(top_builddir) --output-directory coveragereport --title "Code Coverage" --legend --show-details coverage.info

  clean-coverage-html:
	-$(LCOV) --directory $(top_builddir) -z
	-rm -rf coverage.info coveragereport
	-find $(top_builddir) -name '*.gcda' -print | xargs rm

  .PHONY: coverage-xml generate-coverage-xml coverage-xml-clean
  coverage-xml:
	-$(MAKE) $(AM_MAKEFLAGS) -k check
	$(MAKE) $(AM_MAKEFLAGS) generate-coverage-xml

  generate-coverage-xml:
	@echo Generating coverage XML report
	$(MAKE) $(AM_MAKEFLAGS) clean-coverage-xml
	$(GCOVR) -x -r $(top_builddir) -o $(top_builddir)/coverage.xml --object-directory=$(abs_builddir)/.libs

  clean-coverage-xml:
	-rm -rf $(top_builddir)/coverage.xml
endif # HAVE_GCOV

EXTRA_DIST = COPYING.GPL3
