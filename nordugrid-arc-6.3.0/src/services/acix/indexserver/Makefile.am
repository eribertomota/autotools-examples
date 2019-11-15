if SYSV_SCRIPTS_ENABLED
INDEXSERVER_SCRIPT = arc-acix-index
else
INDEXSERVER_SCRIPT =
endif
initd_SCRIPTS = $(INDEXSERVER_SCRIPT)

if SYSTEMD_UNITS_ENABLED
INDEXSERVER_UNIT = arc-acix-index.service
else
INDEXSERVER_UNIT =
endif
units_DATA = $(INDEXSERVER_UNIT)

pkgdata_SCRIPTS = arc-acix-index-start

SUBDIRS = $(TEST_DIR)
dist_SUBDIRS = test
