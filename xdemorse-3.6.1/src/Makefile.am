## Process this file with automake to produce Makefile.in
AM_LDFLAGS = -Wl,--export-dynamic -Wl,--as-needed

AM_CFLAGS = --pedantic -Wall -std=gnu11 -O2 -D_FORTIFY_SOURCE=2 \
			-fstack-protector-strong -Wformat -Werror=format-security -fpie \
			-DGTK_DISABLE_SINGLE_INCLUDES -DGDK_DISABLE_DEPRECATED \
			-DGTK_DISABLE_DEPRECATED -DGSEAL_ENABLE \
			-DGDK_PIXBUF_DISABLE_DEPRECATED -DG_DISABLE_DEPRECATED

AM_CPPFLAGS = \
	-DPROGRAMNAME_LOCALEDIR=\""$(PROGRAMNAME_LOCALEDIR)"\" \
	-DPACKAGE_DATA_DIR=\""$(datadir)"\" \
	-DPACKAGE_LOCALE_DIR=\""$(prefix)/$(DATADIRNAME)/locale"\" \
	@PACKAGE_CFLAGS@

bin_PROGRAMS = xdemorse

xdemorse_SOURCES = \
	callbacks.c	callbacks.h \
	interface.c	interface.h \
	cat.c		cat.h \
	detect.c	detect.h \
	decode.c	decode.h \
	display.c	display.h \
	ifft.c		ifft.h \
	main.c		main.h \
	shared.c	shared.h \
	sound.c		sound.h \
	utils.c		utils.h \
	common.h

if USE_LIBPERSEUS_SDR
  xdemorse_SOURCES += perseus.c perseus.h filters.c filters.h
endif

xdemorse_LDADD = @PACKAGE_LIBS@

