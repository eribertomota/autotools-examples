bin_PROGRAMS=#NAME#
#NAME#_SOURCES=#NAME#.c xmalloc.c system.h aclocal.m4 checkopt.c checkopt.h

#  add " -lm" to the following if #NAME# requires the math library
#NAME#_LDADD=-lopts

EXTRA_DIST=#NAME#.lsm.in #NAME#.spec.in checkopt.def #NAME#.1 manpage.tpl

#  if you write a self-test script named `chk', uncomment the
#  following and add `chk' to the EXTRA_DIST list
#TESTS=chk

#NAME#.o: checkopt.h
checkopt.o: checkopt.c
checkopt.c checkopt.h: $(srcdir)/checkopt.def
	autogen -L/usr/share/autogen $(srcdir)/checkopt.def

#NAME#.1: $(srcdir)/checkopt.def
	autogen -T manpage.tpl  $(srcdir)/checkopt.def
	awk -f updater #NAME#.1 > tmp$$$$ && mv tmp$$$$ #NAME#.1
#	rm updater

# info_TEXINFOS = #NAME#.texinfo
# #NAME#_TEXINFOS = gpl.texinfo

#  install the man page
man_MANS=#NAME#.1
