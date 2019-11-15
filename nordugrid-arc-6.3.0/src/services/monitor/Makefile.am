SUBDIRS = man mon-icons lang includes

monitordir    = @monitor_prefix@
dist_monitor_DATA = $(srcdir)/*.php $(srcdir)/*.js
monitor_DATA = README

install-data-local:
	$(MKDIR_P) $(DESTDIR)$(monitordir)/cache
