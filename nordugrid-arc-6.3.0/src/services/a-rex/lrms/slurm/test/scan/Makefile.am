TESTS = basic-test

TESTS_ENVIRONMENT = \
	PYTHONPATH=$(abs_top_srcdir)/src/utils/python/ \
	ARC_LOCATION=$(abs_builddir) \
	SRCDIR=$(srcdir) \
	$(SHELL) check_scan_script.sh scan-SLURM-job

SCRIPTSNEEDED = check_scan_script.sh \
	scan-SLURM-job $(pkgdatasubdir)/configure-SLURM-env.sh \
	lrms_common.sh $(pkgdatasubdir)/scan_common.sh \
	$(pkglibexecsubdir)/arcconfig-parser \
	command-simulator.sh $(pkglibexecsubdir)/gm-kick

check_SCRIPTS = $(TESTS) $(SCRIPTSNEEDED)

EXTRA_DIST = $(TESTS)

check_scan_script.sh: $(builddir)/../../../test/check_scan_script.sh
	cp $< $@

scan-SLURM-job: $(builddir)/../../scan-SLURM-job
	cp $< $@
	chmod +x $@

$(pkgdatasubdir)/configure-SLURM-env.sh: $(srcdir)/../../configure-SLURM-env.sh
	mkdir -p $(pkgdatasubdir)
	cp $< $@

$(pkgdatasubdir)/scan_common.sh: $(builddir)/../../../scan_common.sh
	mkdir -p $(pkgdatasubdir)
	cp $< $@

lrms_common.sh: $(builddir)/../../../lrms_common.sh
	cp $< $@

$(pkglibexecsubdir)/arcconfig-parser: $(top_builddir)/src/utils/python/arcconfig-parser
	mkdir -p $(pkglibexecsubdir)
	cp $< $@

command-simulator.sh: $(top_srcdir)/src/tests/lrms/command-simulator.sh
	cp $< $@
	chmod +x $@

$(pkglibexecsubdir)/gm-kick: $(srcdir)/../../../test/test-gm-kick.sh
	mkdir -p $(pkglibexecsubdir)
	cp $< $@
	chmod +x $@

CLEANFILES = $(SCRIPTSNEEDED)
