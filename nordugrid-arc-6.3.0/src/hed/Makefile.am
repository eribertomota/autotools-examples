# order is important!
SUBDIRS = libs acc mcc dmc shc daemon identitymap
DIST_SUBDIRS = libs acc mcc dmc shc daemon identitymap

profiledir = $(pkgdatadir)/profiles
profile_DATA = profiles/general/general.xml

profileexampledir = $(pkgdatadir)/examples/config
profileexample_DATA = profiles/*/*.xml

install-profileexampleDATA: $(profile_DATA)
	for i in profiles/*; do \
          profile=`basename $$i` ; \
          mkdir -p "$(DESTDIR)$(profileexampledir)/$$profile" ; \
          ( cd profiles/$$profile ; for i in *.xml ; do \
            test -f $$i && cp -p $$i "$(DESTDIR)$(profileexampledir)/$$profile/" || : ; \
          done ) ; \
        done

uninstall-profileexampleDATA:
	for p in $(profile_DATA); do \
	    p=`echo $$p | sed 's|^\(.*/\)\?profiles/||'`; \
	    rm -f "$(DESTDIR)$(profileexampledir)/$$p"; \
	done
