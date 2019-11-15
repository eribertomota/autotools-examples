configdir = $(datadir)/bbtools
CLEANFILES = bbtoolsrc 

config_DATA =	bbtoolsrc.in \
		bbtime.conf \
		bbtime.style \
		bbtime.nobb \
		README.bbtime

EXTRA_DIST = $(config_DATA)

all-local: bbtoolsrc

bbtoolsrc: bbtoolsrc.in
	@regex_cmd@ -e "s,@configdir@,$(configdir)," bbtoolsrc.in > bbtoolsrc
	
