if SYSV_SCRIPTS_ENABLED
CACHESERVER_SCRIPT = arc-acix-scanner
else
CACHESERVER_SCRIPT =
endif
initd_SCRIPTS = $(CACHESERVER_SCRIPT)

if SYSTEMD_UNITS_ENABLED
CACHESERVER_UNIT = arc-acix-scanner.service
else
CACHESERVER_UNIT =
endif
units_DATA = $(CACHESERVER_UNIT)

pkgdata_SCRIPTS = arc-acix-scanner-start

SUBDIRS = $(TEST_DIR)
dist_SUBDIRS = test
