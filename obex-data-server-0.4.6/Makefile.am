##########
# general / main dir
##########
AM_MAKEFLAGS = --no-print-directory
AM_CFLAGS = @GLIB_CFLAGS@ @BIP_CFLAGS@ @USB_CFLAGS@ @DBUS_CFLAGS@ @BLUEZ_CFLAGS@ @OPENOBEX_CFLAGS@
DISTCLEANFILES =
BUILT_SOURCES =
bin_PROGRAMS =
CLEANFILES =
noinst_PROGRAMS =
EXTRA_DIST = dbus-api.txt


##########
# data dir
##########
configdir   = $(sysconfdir)/obex-data-server
config_DATA = data/capability.xml data/imaging_capabilities.xml

if SYSTEMCONFIG
dbusconfigdir   = $(sysconfdir)/dbus-1/system.d
dbusconfig_DATA = data/obex-data-server.conf
endif

servicedir       = $(datarootdir)/dbus-1/services
service_in_files = data/obex-data-server.service.in
service_DATA     = data/obex-data-server.service

if SYSTEMCONFIG
add_args = --system-bus
endif

$(service_DATA): $(service_in_files) config.log
	$(AM_V_GEN)$(SED) -e "s|\@servicedir\@|$(bindir)|;s|\@add_args\@|$(add_args)|" $< > $@
	
man_MANS = data/obex-data-server.1
	
EXTRA_DIST += data/obex-data-server.1 data/obex-data-server.service.in \
		data/obex-data-server.conf data/capability.xml \
		data/imaging_capabilities.xml

DISTCLEANFILES += data/obex-data-server.service


##########
# src dir
##########
EXTRA_DIST += src/ods-manager.xml src/ods-marshal.list \
		src/ods-server.xml src/ods-server-session.xml \
		src/ods-session.xml

BUILT_SOURCES += src/ods-manager-dbus-glue.h src/ods-marshal.c \
		src/ods-marshal.h src/ods-server-dbus-glue.h \
		src/ods-server-session-dbus-glue.h src/ods-session-dbus-glue.h

bin_PROGRAMS += src/obex-data-server

src_obex_data_server_SOURCES = src/ods-bluez.h src/ods-bluez.c \
				src/ods-usb.c src/ods-usb.h \
				src/ods-capabilities.h src/ods-capabilities.c \
				src/ods-common.h src/ods-common.c \
				src/ods-error.h src/ods-error.c \
				src/ods-folder-listing.h src/ods-folder-listing.c \
				src/ods-imaging-helpers.h src/ods-imaging-helpers.c \
				src/ods-main.c \
				src/ods-marshal.c src/ods-marshal.h \
				src/ods-manager.h src/ods-manager.c \
				src/ods-logging.h src/ods-logging.c \
				src/ods-obex.h src/ods-obex.c \
				src/ods-server.h src/ods-server.c \
				src/ods-server-session.h src/ods-server-session.c \
				src/ods-session.h src/ods-session.c

src_obex_data_server_LDADD = @GLIB_LIBS@ @BIP_LIBS@ @USB_LIBS@ @DBUS_LIBS@ @BLUEZ_LIBS@ @OPENOBEX_LIBS@

src/ods-manager-dbus-glue.h: src/ods-manager.xml
	$(AM_V_GEN)$(DBUS_BINDING_TOOL)	--prefix=ods_manager \
		--mode=glib-server --output=$@ $<

src/ods-server-dbus-glue.h: src/ods-server.xml
	$(AM_V_GEN)$(DBUS_BINDING_TOOL) --prefix=ods_server \
		--mode=glib-server --output=$@ $<

src/ods-server-session-dbus-glue.h: src/ods-server-session.xml
	$(AM_V_GEN)$(DBUS_BINDING_TOOL) --prefix=ods_server_session \
		--mode=glib-server --output=$@ $<

src/ods-session-dbus-glue.h: src/ods-session.xml
	$(AM_V_GEN)$(DBUS_BINDING_TOOL) --prefix=ods_session \
		--mode=glib-server --output=$@ $<

src/ods-marshal.c: src/ods-marshal.list
	$(AM_V_GEN)@GLIB_GENMARSHAL@ $< --prefix=ods_marshal --body > $@

src/ods-marshal.h: src/ods-marshal.list
	$(AM_V_GEN)@GLIB_GENMARSHAL@ $< --prefix=ods_marshal --header > $@
	
CLEANFILES += $(BUILT_SOURCES)


##########
# test dir
##########
noinst_PROGRAMS += test/ods-dbus-test

test_ods_dbus_test_SOURCES = src/ods-marshal.h src/ods-marshal.c \
				test/ods-dbus-test.c

test_ods_dbus_test_LDADD = @GLIB_LIBS@ @DBUS_LIBS@ @BLUEZ_LIBS@
	
EXTRA_DIST += test/ods-server-test.py test/ods-session-test.py \
		test/ods-bip-test.py test/ods-opp-test.py

