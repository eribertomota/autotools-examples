TESTS_ENVIRONMENT = \
	PYTHONPATH=$(abs_top_builddir)/python/python:$(abs_top_builddir)/python/python/arc/.libs:$(abs_top_srcdir)/src/services/a-rex/infoproviders \
	$(PERL) $(PERL5LIB_INLINE_PYTHON) -I$(srcdir) -I$(srcdir)/.. -w -MTest::Harness -e '$$Test::Harness::verbose=0; runtests @ARGV;'

if PYTHON_LRMS_ENABLED
    SLURMPY_TEST = slurmpy.t
else
    SLURMPY_TEST =
endif

TESTS = pbs.t slurm.t $(SLURMPY_TEST) sge.t

PERL = @PERL@

check_SCRIPTS = InfoproviderTestSuite.pm command-simulator.sh \
                $(TESTS)

EXTRA_DIST = InfoproviderTestSuite.pm command-simulator.sh pbs.t slurm.t slurmpy.t sge.t

command-simulator.sh: $(top_srcdir)/src/tests/lrms/command-simulator.sh
	cp $< $@
	chmod +x $@
