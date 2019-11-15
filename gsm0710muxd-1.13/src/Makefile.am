usrsbindir = ${exec_prefix}/sbin

usrsbin_PROGRAMS = gsm0710muxd

gsm0710muxd_SOURCES = muxercontrol.c gsm0710muxd.c

gsm0710muxd_LDADD = @DBUS_GLIB_LIBS@ @DBUS_LIBS@ @GLIB_LIBS@

AM_CFLAGS = @GLIB_CFLAGS@ @DBUS_CFLAGS@ @DBUS_GLIB_CFLAGS@

nodist_gsm0710muxd_SOURCES = $(BUILT_SOURCES)

EXTRA_DIST = muxercontrol.vala gsm0710muxd.vapi

MAINTAINERCLEANFILES = Makefile.in

muxercontrol.c: muxercontrol.vala
	$(VALAC) --vapidir=$(top_srcdir)/src --pkg=gsm0710muxd --pkg=dbus-glib-1 --ccode $<
