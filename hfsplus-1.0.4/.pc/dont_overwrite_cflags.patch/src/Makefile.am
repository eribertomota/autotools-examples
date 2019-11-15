#
# Makefile.am for hfsplus
#
# Created by Klaus Kaempf <kkaempf@suse.de> and
#	     Klaus Halfmann <klaus.halfmann@feri.de>
#
# $Id: Makefile.am,v 1.1.1.1 2002/03/05 19:50:29 klaus Exp $

INCLUDES = -I../libhfsp/src

CFLAGS = -O2 -Wall

bin_PROGRAMS = hpmount hpumount hpls hpcd hpcopy hppwd hpfsck hprm hpmkdir

hpmount_SOURCES = hpmount.c hpcache.c hfsputil.c glob.c dstring.c dlist.c

hpumount_SOURCES = hpumount.c hpcache.c hfsputil.c glob.c dstring.c dlist.c

hpls_SOURCES =  hpls.c dstring.c dlist.c darray.c glob.c hpcache.c hfsputil.c

hpcd_SOURCES =  hpcd.c dstring.c dlist.c glob.c hpcache.c hfsputil.c

hppwd_SOURCES =  hppwd.c dstring.c hpcache.c hfsputil.c glob.c dlist.c

hpcopy_SOURCES = hpcopy.c hpcache.c charset.c copyout.c binhex.c crc.c hfsputil.c glob.c \
		 dstring.c dlist.c

hprm_SOURCES = hprm.c hpcache.c charset.c hfsputil.c glob.c dstring.c dlist.c

hpmkdir_SOURCES = hpmkdir.c hpcache.c charset.c hfsputil.c glob.c dstring.c dlist.c

hpfsck_SOURCES = hpfsck.c hfsputil.c glob.c dstring.c dlist.c

LDADD = ../libhfsp/src/libhfsp.la

# dynamically linked tools dont work, yet ..
# LDADD = ../libhfsp/src/libhfsp.la

AUTOMAKE_OPTIONS = foreign

CLEANFILES = config.cache config.status config.log

MAINTAINERCLEANFILES = Makefile Makefile.in \
	configure config.h config.sub config.guess \
	ltconfig ltmain.sh stamp-h stamp-h.in libtool aclocal.m4
