TESTSCRIPTS = test_cacheresource.py test_scan.py

if ACIX_TESTS_ENABLED
TESTS_ENVIRONMENT = PYTHONPATH=$(top_srcdir)/src/services:${top_srcdir}/src/utils/python $(TRIAL)
TESTS = $(TESTSCRIPTS)
else
TESTS =
endif

check_SCRIPTS = $(TESTS)

EXTRA_DIST = $(TESTSCRIPTS)
