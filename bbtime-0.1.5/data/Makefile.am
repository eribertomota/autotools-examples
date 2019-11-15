configdir = $(sysconfdir)/bbtools
CLEANFILES = bbtoolsrc 

config_DATA =	bbtime.conf \
		bbtime.style \
		bbtime.nobb

EXTRA_DIST = $(config_DATA) bbtoolsrc.in

all-local: bbtoolsrc

bbtoolsrc: bbtoolsrc.in
	@regex_cmd@ -e "s,@configdir@,$(configdir)," bbtoolsrc.in > bbtoolsrc
	
