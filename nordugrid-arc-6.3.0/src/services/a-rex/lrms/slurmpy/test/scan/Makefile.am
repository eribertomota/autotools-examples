TESTS = basic-test

TESTS_ENVIRONMENT = \
	PERL5LIB=$(abs_top_srcdir)/src/services/a-rex/infoproviders \
	PYTHONPATH=$(abs_top_builddir)/python/python:$(abs_top_builddir)/python/python/arc/.libs:$(abs_top_srcdir)/src/services/a-rex/lrms \
	ARC_LOCATION=$(abs_builddir) \
	SRCDIR=$(srcdir) \
	$(SHELL) check_scan_script.sh scan-SLURMPY-job

SCRIPTSNEEDED = check_scan_script.sh scan-SLURMPY-job \
	command-simulator.sh $(pkglibexecsubdir)/gm-kick

check_SCRIPTS = $(TESTS) $(SCRIPTSNEEDED)

EXTRA_DIST = $(TESTS)

check_scan_script.sh: $(builddir)/../../../test/check_scan_script.sh
	cp $< $@

scan-SLURMPY-job: $(builddir)/../../scan-SLURMPY-job
	cp $< $@
	chmod +x $@

command-simulator.sh: $(top_srcdir)/src/tests/lrms/command-simulator.sh
	cp $< $@
	chmod +x $@

$(pkglibexecsubdir)/gm-kick: $(srcdir)/../../../test/test-gm-kick.sh
	mkdir -p $(pkglibexecsubdir)
	cp $< $@
	chmod +x $@

CLEANFILES = $(SCRIPTSNEEDED)
