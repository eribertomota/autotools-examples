bin_PROGRAMS=#NAME#
#NAME#_SOURCES=#NAME#.c xmalloc.c system.h aclocal.m4 #NAME#.1 cmdline.c cmdline.h

#  uncomment the following if #NAME# requires the math library
##NAME#_LDADD=-lm

EXTRA_DIST=#NAME#.lsm.in #NAME#.spec.in cmdline.cli.in

#  if you write a self-test script named `chk', uncomment the
#  following and add `chk' to the EXTRA_DIST list
#TESTS=chk

#NAME#.o: cmdline.h
cmdline.o: cmdline.c
cmdline.c cmdline.h: cmdline.cli.in
	$(MAKE) cmdline.cli
	clig cmdline.cli

# clig does not support .info pages
# info_TEXINFOS = #NAME#.texinfo
# #NAME#_TEXINFOS = gpl.texinfo

#  install the man page
man_MANS=#NAME#.1
