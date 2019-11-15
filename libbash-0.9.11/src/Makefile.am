AUTOMAKE_OPTIONS = -Wno-portability

EXTRA_DIST = $(wildcard *.in) $(wildcard *.man)

bin_SCRIPTS = ldbash

sbin_SCRIPTS = ldbashconfig

# This creates $(sysconfdir). If this will not be here, the ldbashconfig command will fail.
sysconf_DATA = 

CLEANFILES = ldbash ldbashconfig

# installing man pages
man1_MANS = ldbash.man
man8_MANS = ldbashconfig.man

