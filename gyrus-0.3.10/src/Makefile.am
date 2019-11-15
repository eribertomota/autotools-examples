## Process this file with automake to produce Makefile.in

SUBDIRS = \
	ui \
	pixmaps

uidir = $(datadir)/gyrus/ui
pixmapsdir = $(datadir)/gyrus/pixmaps

INCLUDES = \
	-DGYRUS_DATA_DIR=\""$(datadir)"\" \
	-DGYRUS_UI_DIR=\""$(uidir)"\" \
	-DGYRUS_PIXMAPS_DIR=\""$(pixmapsdir)"\" \
	-DGNOME_LOCALE_DIR=\""$(prefix)/$(DATADIRNAME)/locale"\" \
	$(GYRUS_CFLAGS)

bin_PROGRAMS = gyrus

EXTRA_DIST =  \
	gyrus-marshal.list

BUILT_SOURCES = \
	gyrus-marshal.c gyrus-marshal.h

DISTCLEANFILES = $(BUILT_SOURCES)

gyrus_LDFLAGS = -export-dynamic

gyrus_SOURCES = \
	gyrus-admin.c gyrus-admin.h \
	gyrus-admin-private.h \
	gyrus-admin-mailbox.c gyrus-admin-mailbox.h \
	gyrus-admin-acl.c gyrus-admin-acl.h \
	gyrus-common.c gyrus-common.h \
	gyrus-dialog-find-mailbox.c gyrus-dialog-find-mailbox.h \
	gyrus-dialog-mailbox-new.c gyrus-dialog-mailbox-new.h \
	gyrus-main-app.c gyrus-main-app.h \
	gyrus-marshal.c gyrus-marshal.h \
	gyrus-report.c gyrus-report.h \
	gyrus-session.c gyrus-session.h


gyrus_LDADD = $(GYRUS_LIBS)

gyrus-marshal.h: gyrus-marshal.list $(GLIB_GENMARSHAL)
	$(GLIB_GENMARSHAL) $< --header --prefix=gyrus > $@

gyrus-marshal.c: gyrus-marshal.list $(GLIB_GENMARSHAL)
	echo "#include \"gyrus-marshal.h\"" > $@ && \
	$(GLIB_GENMARSHAL) $< --body --prefix=gyrus >> $@
