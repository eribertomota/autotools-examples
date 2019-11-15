dist_sbin_SCRIPTS = nordugridmap

cronddir = @cronddir@

man_MANS = nordugridmap.8

# Not using crond_DATA since we need to rename it.
install-exec-local:
	$(MKDIR_P) "$(DESTDIR)$(cronddir)"
	$(INSTALL_DATA) nordugridmap.cron $(DESTDIR)$(cronddir)/nordugridmap
uninstall-local:
	rm -f $(DESTDIR)$(cronddir)/nordugridmap
