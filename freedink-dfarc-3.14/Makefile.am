AUTOMAKE_OPTIONS = gnits

# src/ before po/, so wxglade can generate some translatable source
# files first.
SUBDIRS = src share po

# Copy those directly and recursively:
# Build system
EXTRA_DIST = bootstrap m4/ChangeLog
# Documentation
EXTRA_DIST += doc
EXTRA_DIST += BUILD COPYING.DFArc COPYING.DFArc-2.0 TRANSLATIONS.txt
# Packaging
EXTRA_DIST += debian freedink-dfarc.spec

dist-hook:
	find $(distdir) -name '*~' | xargs -r rm -f
#	Prepare some files with MS-DOS newlines to ship in woe releases
#	At the end of each line (doubled $), add a \r, so we get \r\n
	cd $(distdir) && sed 's/$$/\r/' README > README.txt
#	Force inclusion of the translation template
	-cp "$(srcdir)/po/$(GETTEXT_PACKAGE).pot" "$(builddir)/po" # avoid ../.. rule
	$(MAKE) -C "$(builddir)/po" "$(GETTEXT_PACKAGE).pot"
	cp "$(builddir)/po/$(GETTEXT_PACKAGE).pot" "$(distdir)/po/"

ACLOCAL_AMFLAGS = -I m4

version:
	@echo $(VERSION)
