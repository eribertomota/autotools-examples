## Process this file with automake to produce Makefile.in

check_SCRIPTS=test-prep-1 test-2utf8-1 test-2utf8-2 \
	                  test-2beta-1 test-2beta-2
TESTS=$(check_SCRIPTS)
EXTRA_DIST=$(check_SCRIPTS) test-all
AM_TESTS_ENVIRONMENT = unibetacode_path='$(abs_top_builddir)/src' ; \
	export unibetacode_path ;

installcheck-local:
	make unibetacode_bindir=${DESTDIR}${bindir} check
