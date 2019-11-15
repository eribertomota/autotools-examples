## Process this file with automake to produce Makefile.in

INCLUDES = -Wall \
	-DPACKAGE_DATA_DIR=\""$(datadir)"\" \
	-DPACKAGE_LOCALE_DIR=\""$(prefix)/$(DATADIRNAME)/locale"\" \
	-DPACKAGE_SYSCONFIGDIR=\""$(sysconfdir)"\" \
	@PACKAGE_CFLAGS@ @LASH_CFLAGS@

bin_PROGRAMS = gjacktransport gjackclock

EXTRA_DIST = gjt_icon.xpm gjc_icon.xpm gjacktransportrc gjackclockrc

gjacktransport_SOURCES = \
	main.c gjacktransport.h \
	support.c support.h \
	interface.c interface.h \
	callbacks.c callbacks.h \
	framerate.c framerate.h \
	gjack.c gjack.h \
	lash.c resourceconfig.c rc_gjt.c

gjacktransport_LDADD = @PACKAGE_LIBS@ $(INTLLIBS) @LASH_LIBS@ -lm
gjacktransport_CFLAGS = -DGJACKTRANSPORTRC=\"gjacktransportrc\"

gjackclock_SOURCES = \
	gjackclock.c gjackclock.h \
	framerate.c framerate.h \
	resourceconfig.c rc_gjc.c

gjackclock_LDADD = @PACKAGE_LIBS@ $(INTLLIBS) @LASH_LIBS@ -lm
gjackclock_CFLAGS = -DGJACKTRANSPORTRC=\"gjackclockrc\"
