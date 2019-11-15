dbusdir = $(sysconfdir)/dbus-1/system.d
initdir = $(sysconfdir)/init.d

dist_dbus_DATA = gsm0710muxd.conf
dist_init_SCRIPTS = gsm0710muxd

servicedir = $(datadir)/dbus-1/system-services

service_in_files = org.pyneo.muxer.service.in

service_DATA = $(service_in_files:.service.in=.service)

CLEANFILES = $(service_DATA)

EXTRA_DIST = $(service_in_files)

MAINTAINERCLEANFILES = Makefile.in

$(service_DATA): $(service_in_files)
	@sed -e "s|\@sbindir\@|$(sbindir)|" $<> $@
