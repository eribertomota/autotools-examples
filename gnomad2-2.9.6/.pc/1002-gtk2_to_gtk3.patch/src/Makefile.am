MAINTAINERCLEANFILES = Makefile.in

INCLUDES = \
	@GN_CFLAGS@ \
	@TAG_CFLAGS@ \
	@MTP_CFLAGS@ \
	@TAGLIB_CFLAGS@ \
	@GUDEV_CFLAGS@ \
	-DPREFIX=\"$(prefix)\" \
	-DSYSCONFDIR=\"$(sysconfdir)\" \
	-DDATADIR=\"$(datadir)\" \
	-DLIBDIR=\"$(libdir)\" \
	-DPIXMAPSDIR=\""$(datadir)/pixmaps"\"

LDADD = \
	@GN_LIBS@ \
	@TAG_LIBS@ \
	@MTP_LIBS@ \
	@TAGLIB_LIBS@ \
	@GUDEV_LIBS@

bin_PROGRAMS = gnomad2

gnomad2_SOURCES = id3read.c id3read.h \
		gnomad2.c prefs.c prefs.h \
		filenaming.c filenaming.h jukebox.c jukebox.h \
		util.c util.h \
		mp3file.c mp3file.h \
		editmeta.c editmeta.h filesystem.c filesystem.h \
		playlists.c playlists.h xfer.c xfer.h \
		data.c data.h player.c player.h common.h \
		metadata.c metadata.h \
		wmaread.c wmaread.h \
		riffile.c riffile.h

if TAGLIB_COMPILE
gnomad2_SOURCES += tagfile.c tagfile.h
endif