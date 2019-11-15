#
#  NASPRO - The NASPRO Architecture for Sound Processing
#  Common headers for all ino implementations
#
#  Copyright (C) 2011, 2012 ino development team
#
#  See the COPYING file for license conditions.
#

if BUILD_DOC

.PHONY: html

html:
	$(MKDIR_P) html
	@if [ ! "$(top_srcdir)/doc" -ef . ]; then \
		echo cp -fpR \"$(top_srcdir)/doc/proj\" proj; \
		cp -fpR "$(top_srcdir)/doc/proj" proj; \
	fi
	$(NATURALDOCS) -i "$(top_srcdir)" -o html html -p proj

install-data-local:
	@if [ -d html ]; then \
		echo $(mkinstalldirs) \"$(DESTDIR)$(docdir)/html\"; \
		$(mkinstalldirs) "$(DESTDIR)$(docdir)/html"; \
		oldIFS="$$IFS"; \
		IFS=$$'\n'; \
		for d in `find html -type d`; do \
			echo $(mkinstalldirs) \"$(DESTDIR)$(docdir)/$$d\"; \
			$(mkinstalldirs) "$(DESTDIR)$(docdir)/$$d"; \
			for f in `ls -1 "$$d"`; do \
				[ -f "$$d/$$f" ] || continue; \
				echo $(INSTALL_DATA) \"$$d/$$f\" \"$(DESTDIR)$(docdir)/$$d/$$f\" ; \
				$(INSTALL_DATA) "$$d/$$f" "$(DESTDIR)$(docdir)/$$d/$$f"; \
			done; \
		done; \
		IFS="$$oldIFS"; \
	fi

uninstall-local:
	-rm -fr "$(DESTDIR)$(docdir)"

clean-local:
	-rm -fr html proj/Data

endif

EXTRA_DIST = proj/Languages.txt proj/Menu.txt proj/Topics.txt
