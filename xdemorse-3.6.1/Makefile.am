## Process this file with automake to produce Makefile.in

SUBDIRS = src po

EXTRA_DIST = \
			 autogen.sh \
			 .xdemorse \
			 files \
			 doc

DISTCLEANFILES = \
				 autom4te.cache/* \
				 intl/* \
				 m4/* \
				 aclocal.m4 \
				 compile \
				 config.guess \
				 config.rpath \
				 config.status \
				 config.sub \
				 configure \
				 depcomp \
				 install-sh \
				 missing \
				 ABOUT-NLS \
				 Makefile.in \
				 config.h \
				 config.h.in \
				 config.log \
				 configure \
				 stamp-h1 \
				 stamp-h.in \
				 src/Makefile.in \
				 po/Rules-quot \
				 po/en@quot.header \
				 po/remove-potcdate.sin \
				 po/Makevars.template \
				 po/boldquot.sed \
				 po/insert-header.sin \
				 po/stamp-po \
				 po/en@boldquot.header \
				 po/quot.sed \
				 po/Makefile.in.in \
				 po/xdemorse.pot \
				 Makefile

DISABLE-install-data-local:
	@$(NORMAL_INSTALL)
	if test -d files/; then \
	  cp files/$(PACKAGE).desktop $(DESTDIR)/usr/share/applications/; \
	  cp files/$(PACKAGE).png $(DESTDIR)/usr/share/pixmaps/; \
	fi; \
	if !(test -d $(DESTDIR)/usr/share/doc/$(PACKAGE)); then \
	  mkdir $(DESTDIR)/usr/share/doc/$(PACKAGE)/; \
	fi; \
	if test -d doc/; then \
	  cp -r doc/* $(DESTDIR)/usr/share/doc/$(PACKAGE)/; \
	  cp -r doc/$(PACKAGE).1.gz $(DESTDIR)/usr/share/man/man1/; \
	fi; \
	if !(test -d /home/`logname`/.$(PACKAGE)); then \
	  cp -r .$(PACKAGE) /home/`logname`/; \
	else \
	  cp .$(PACKAGE)/$(PACKAGE).glade /home/`logname`/.$(PACKAGE); \
	fi; \
	chown -R `logname`:`logname` /home/`logname`/.$(PACKAGE);

