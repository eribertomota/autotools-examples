# $Header: /cvs/rfdump/src/Makefile.am,v 1.19 2008/06/13 03:13:41 doj Exp $

INCLUDES = @GTK2_CFLAGS@ @LIBGLADE_CFLAGS@

bin_PROGRAMS = rfdump

rfdump_SOURCES = \
	main.c main.h tools.h \
	callbacks.c mifare.c \
	rfid.c rfid.h \
	tagtypes.c tagtypes.h \
	xml.c xml.h \
	acg.c acg.h \
	tcpconnect.c

rfdump_LDFLAGS=-rdynamic
rfdump_LDADD = @GTK2_LIBS@ @LIBGLADE_LIBS@

rfdumpdir = $(prefix)/share/rfdump
rfdump_DATA = rfd.dtd rfd_types.xml rfdump.glade rfdump.gladep mifare.txt rfdump.png rfdump.xpm
EXTRA_DIST =  rfd.dtd rfd_types.xml rfdump.glade rfdump.gladep mifare.txt rfdump.png rfdump.xpm rfdump.desktop

# this is the Gnome Application Icon, because we don't know it better currently hardcoded directory name
pixmapdir = /usr/share/pixmaps
pixmap_DATA = rfdump.png

# the Gnome Application config
Applicationsdir = $(prefix)/share/applications
Applications_DATA = rfdump.desktop

CFLAGS = -Wall @CFLAGS@ -DVERSION=\"@VERSION@\"
