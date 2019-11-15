TESTS = basic-test memory-test count-test queue-test job-name-test \
	cpu-wall-time-test rte-test config-options-test std-io-test

TESTS_ENVIRONMENT = \
	PERL5LIB=$(abs_top_srcdir)/src/services/a-rex/infoproviders \
	PYTHONPATH=$(abs_top_builddir)/python/python:$(abs_top_builddir)/python/python/arc/.libs \
	ARC_PLUGIN_PATH=$(abs_top_builddir)/src/hed/acc/JobDescriptionParser/.libs \
	ARC_LOCATION=$(abs_builddir) \
	TEST_WRITE_GRAMI_FILE=$(top_builddir)/src/services/a-rex/grid-manager/test_write_grami_file \
	SRCDIR=$(srcdir) \
	$(SHELL) check_submit_script.sh submit-SLURMPY-job

SCRIPTSNEEDED = check_submit_script.sh \
	submit-SLURMPY-job $(builddir)/share/arc/job_script.stubs

check_SCRIPTS = $(TESTS) basic-script.sh $(SCRIPTSNEEDED)

EXTRA_DIST = $(TESTS) basic-script.sh

check_submit_script.sh: $(srcdir)/../../../test/check_submit_script.sh
	cp $< $@

submit-SLURMPY-job: $(builddir)/../../submit-SLURMPY-job
	cp $< $@
	chmod +x $@

$(builddir)/share/arc/job_script.stubs: $(srcdir)/../../../arc/lrms/common/job_script.stubs
	mkdir -p $(builddir)/share/arc
	cp $< $@

CLEANFILES = $(SCRIPTSNEEDED)
