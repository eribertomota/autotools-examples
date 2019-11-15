## Process this file with automake to produce Makefile.in

INCLUDES = \
	-DPACKAGE_DATA_DIR=\""$(datadir)"\" \
	-DPACKAGE_LOCALE_DIR=\""$(prefix)/$(DATADIRNAME)/locale"\" \
	@PACKAGE_CFLAGS@

jackeq_CFLAGS = -g -ffast-math

bin_PROGRAMS = jackeq

jackeq_SOURCES = \
	callbacks.c callbacks.h callbacks_help.h \
	db.h \
	debug.h \
	gtkmeter.c gtkmeter.h \
	gtkmeterscale.c gtkmeterscale.h \
	interface.c interface.h \
	io-menu.c io-menu.h \
	djeq.h \
	djeq-ui.c djeq-ui.h \
	aux-ui.c aux-ui.h \
	master-ui.c master-ui.h \
	monitor-ui.c monitor-ui.h \
	main.c main.h \
	plugin.c plugin.h \
	process.c process.h \
	support.c support.h \
	help.c help.h

jackeq_LDADD = @PACKAGE_LIBS@ -lm -ldl
