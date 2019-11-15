check_SCRIPTS=test1 test2 test3
TESTS=$(check_SCRIPTS)
EXTRA_DIST=README-test $(check_SCRIPTS) test-all sample-in.txt \
 sample1-out.txt sample2-out.txt sample3-out.txt
AM_TESTS_ENVIRONMENT = utf8gen_path='$(abs_top_builddir)/src' ; \
	export utf8gen_path ;

installcheck-local:
	make utf8gen_bindir=${DESTDIR}${bindir} check
