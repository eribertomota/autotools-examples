AUTOMAKE_OPTIONS = gnits
# Gnulib + other macros (keep on a single line)
ACLOCAL_AMFLAGS = -I gnulib/m4  -I autotools/m4

SUBDIRS = gnulib/lib gnulib/po nsis po src share

# Copy those directly and recursively:
# Build system
EXTRA_DIST = bootstrap gnulib/m4/gnulib-cache.m4
# Documentation
EXTRA_DIST += doc
EXTRA_DIST += BUILD TRANSLATIONS.txt TROUBLESHOOTING
# Packaging
EXTRA_DIST += debian freedink.spec
# Other programs of interest
EXTRA_DIST += contrib
# Android
EXTRA_DIST += android
# Emscripten
EXTRA_DIST += emscripten

dist-hook:
	find $(distdir) -name '*~' | xargs -r rm -f
#	Remove .gitignore files; e.g. they prevent 'git-buildpackage'
#	from importing ignored files from release tarballs
	find $(distdir) -name '.gitignore' | xargs -r rm -f
#	At the end of each line (doubled $), add a \r, so we get \r\n
	cd $(distdir) && sed 's/$$/\r/' README > README.txt
#	Remove Android generated files
	cd $(distdir)/android/ && make distclean

version:
	@echo $(VERSION)
