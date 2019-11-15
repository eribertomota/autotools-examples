
SIGNER = stef@thewalter.net
UPLOAD = thewalter.net:/data/www/stef/software/proxsmtp
FRESHMEAT = freshmeat.rel

EXTRA_DIST = config.sub acsite.m4 config.guess scripts common
SUBDIRS = src doc

dist-hook:
	@if test -d "$(srcdir)/.git"; \
	then \
		echo Creating ChangeLog && \
		( cd "$(top_srcdir)" && \
		  echo '# Generate automatically. Do not edit.'; echo; \
		  $(top_srcdir)/missing --run git log --stat --date=short ) > ChangeLog.tmp \
		&& mv -f ChangeLog.tmp $(top_distdir)/ChangeLog \
		|| ( rm -f ChangeLog.tmp ; \
		     echo Failed to generate ChangeLog >&2 ); \
	else \
		echo A git clone is required to generate a ChangeLog >&2; \
	fi
	@if test -f $(srcdir)/$(FRESHMEAT); then \
		grep -qF "$(PACKAGE_VERSION)" $(srcdir)/$(FRESHMEAT) || \
			( echo "$(FRESHMEAT) release not updated" >&2; exit 1 ); \
	fi

upload-release: $(DIST_ARCHIVES)
	gpg --detach-sign --local-user $(SIGNER) $(DIST_ARCHIVES)
	scp $(DIST_ARCHIVES) $(DIST_ARCHIVES).sig $(FRESHMEAT) NEWS $(UPLOAD)
	@echo
	@echo "# Remember to update $(UPLOAD)/index.html"

