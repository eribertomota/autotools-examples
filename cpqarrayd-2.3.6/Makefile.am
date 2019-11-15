SUBDIRS = scripts
sbin_PROGRAMS = cpqarrayd
cpqarrayd_SOURCES = cpqarrayd.c discover.c sendtrap.c status.c cciss_functions.c cciss_functions.h config.h discover.h status.h cciss_structs.h cpqarrayd.h sendtrap.h
EXTRA_DIST = cpqarrayd.spec
dist_man_MANS = cpqarrayd.1

install-redhat:
	( cd scripts && $(MAKE) $(AM_MAKEFLAGS) install-redhat )

uninstall-redhat:
	( cd scripts && $(MAKE) $(AM_MAKEFLAGS) uninstall-redhat )
