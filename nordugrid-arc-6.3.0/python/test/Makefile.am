if ALTPYTHON_ENABLED
ALTPYTHON_DIR = altpython
else
ALTPYTHON_DIR =
endif

DIST_SUBDIRS = python altpython
SUBDIRS = python $(ALTPYTHON_DIR)

include tests.mk

EXTRA_DIST = $(TESTSCRIPTS) $(AUXFILES) common.mk
