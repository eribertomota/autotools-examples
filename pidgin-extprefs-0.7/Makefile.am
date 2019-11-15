EXTRA_DIST =                 \
	ChangeLog            \
	INSTALL              \
	INSTALL-win32.txt    \
	LICENSE              \
	Makefile.mingw       \
	TODO                 \
	src/Makefile.mingw

SUBDIRS = src

DISTCLEANFILES = extprefs_config.h

BUILT_SOURCES = extprefs_config.h

$(OBJECTS): $(BUILT_SOURCES)

extprefs_config.h: pre_config.h
	$(sedpath) 's/#define PACKAGE/#define EXTPREFS_PACKAGE/g' pre_config.h > $@
