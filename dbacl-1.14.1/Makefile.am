AUTOMAKE_OPTIONS = 1.4 gnits
ACLOCAL = -I config

AUX_DIST = config/config.guess \
	config/config.sub \
	config/install-sh \
	config/missing \
	config/mkinstalldirs

EXTRA_DIST = bootstrap

SUBDIRS = doc src man ts TREC contrib

# fix for new auto{conf,make} behaviour ???
datarootdir ?= $(prefix)/share
dist-hook:
	(cd $(distdir) && mkdir -p config)
	for f in $(AUX_DIST); do \
		cp $$f $(distdir)/$$f; \
	done

trec:
	make dist && (cat TREC/SFX $(distdir).tar.gz > $(distdir).TREC.sfx.sh)
	test -e $(distdir).TREC.sfx.sh && chmod +x $(distdir).TREC.sfx.sh
