## Process this file with automake to produce Makefile.in

check_SCRIPTS=test-ascii \
	test-utf8 test-utf8-bom-begin test-utf8-bom-end \
	test-binary test-utf16-be test-utf16-le \
	test-ascii-only test-utf8-expurgated test-utf8-surrogate
TESTS=$(check_SCRIPTS)

EXTRA_DIST=$(check_SCRIPTS) init-out test-all samples expected
dist-hook:
	rm -rf $(distdir)/test/samples/gen-utf

AM_TESTS_ENVIRONMENT = utfcheck_path='$(abs_top_builddir)/src' ; \
	export utfcheck_path ;

installcheck-local:
	make utfcheck_bindir=${DESTDIR}${bindir} check

maintainer-clean-local:
	\rm -f *.log *.trs
	\rm -f samples/gen-utf
