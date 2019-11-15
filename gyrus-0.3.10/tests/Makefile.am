#Makefile.am for the gyrus tests.

EXTRA_DIST =	\
	gyrus-talk.xml

INCLUDES = \
	-DGYRUS_DATA_DIR=\""$(datadir)"\" \
	-DGNOME_LOCALE_DIR=\""$(prefix)/$(DATADIRNAME)/locale"\" \
	$(GYRUS_CFLAGS) \
	-I$(top_srcdir)/src/

noinst_PROGRAMS = 	\
	gyrus-talk

gyrus_talk_LDFLAGS = -export-dynamic

gyrus_talk_SOURCES = \
	gyrus-talk.c

gyrus_talk_LDADD = $(GYRUS_LIBS) \
	$(top_builddir)/src/gyrus-connection.o   \
	$(top_builddir)/src/gyrus-marshal.o
