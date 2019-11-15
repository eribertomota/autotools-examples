SUBDIRS = man
data_DATA = cpu.conf.doc test.ldif
EXTRA_DIST = cpu.conf \
	cpu.conf.doc \
	test.ldif
sysconfdir = ../debian/cpu/usr/share/cpu

install-data-local:
	@if test -f $(sysconfdir)/cpu.conf ; then \
		echo "$@ will not overwrite existing $(sysconfdir)/cpu.conf"; \
	else \
		$(mkinstalldirs) $(sysconfdir); \
		echo "$(INSTALL_DATA) cpu.conf $(sysconfdir)/cpu.conf"; \
		$(INSTALL_DATA) cpu.conf $(sysconfdir)/cpu.conf; \
	fi

uninstall-local:
	@if test -f $(sysconfdir)/cpu.conf ; then \
		echo "rm -f $(sysconfdir)/cpu.conf"; \
		$(RM) -f $(sysconfdir)/cpu.conf; \
	fi
