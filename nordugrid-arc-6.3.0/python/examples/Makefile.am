if MACOSX
DYLD_LIBRARY_PATH = "$(top_builddir)/src/hed/libs/credentialstore/.libs:$(top_builddir)/src/hed/libs/communication/.libs:$(top_builddir)/src/hed/libs/compute/.libs:$(top_builddir)/src/hed/libs/data/.libs:$(top_builddir)/src/hed/libs/security/.libs:$(top_builddir)/src/hed/libs/credential/.libs:$(top_builddir)/src/hed/libs/crypto/.libs:$(top_builddir)/src/hed/libs/message/.libs:$(top_builddir)/src/hed/libs/loader/.libs:$(top_builddir)/src/hed/libs/common/.libs:$(top_builddir)/src/libs/data-staging/.libs"
else
DYLD_LIBRARY_PATH =
endif

EXAMPLES = \
	basic_job_submission.py partial_copy.py copy_file.py job_filtering.py \
	joblist_retrieval.py job_status.py job_submission.py retrieving_results.py \
	service_discovery.py dtr_generator.py job_selector.py

if PYLINT_ENABLED
# Any options to arguments to pylint should be defined and checked in configure.
TESTS_ENVIRONMENT = \
	ARC_PLUGIN_PATH=$(top_builddir)/src/hed/acc/TEST/.libs \
	DYLD_LIBRARY_PATH="$(DYLD_LIBRARY_PATH)" \
	PYTHONPATH="../python:../python/arc/.libs" \
	$(PYLINT) $(PYLINT_ARGS) $(PYLINT_ARGS_ARGUMENTS_DIFFER)
TESTS = $(EXAMPLES)
else
TESTS =
endif

check_SCRIPTS = $(EXAMPLES)

exampledir = $(pkgdatadir)/examples/sdk
example_DATA = $(EXAMPLES)

EXTRA_DIST = $(EXAMPLES)
