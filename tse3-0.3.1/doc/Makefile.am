###############################################################################
# These are the distribution files

EXTRA_DIST =                     \
	History                      \
	src/About.html.in            \
	src/Article.html.in          \
	src/Build.html.in            \
	src/Bugs.html.in             \
	src/Commands.html.in         \
	src/Copyright.html.in        \
	src/Error.html.in            \
	src/Examples.html.in         \
	src/Feedback.html.in         \
	src/HOWTO.html.in            \
	src/History.html.in          \
	src/InsFiles.html.in         \
	src/KDOC.html.in             \
	src/Mutex.html.in            \
	src/Notifier.html.in         \
	src/Playable.html.in         \
	src/Porting.html.in          \
	src/Psalm150.html.in         \
	src/Song.html.in             \
	src/Structure.html.in        \
	src/TSE3MDL.html.in          \
	src/Trax.html.in             \
	src/Trouble.html.in          \
	src/Whitepaper.html.in       \
	src/Version.html.in          \
	src/htmlize.pl               \
	src/index.html.in            \
	src/pete.jpeg.verbatim.in    \
	src/trax.gif.verbatim.in     \
	src/tse3.gif.verbatim.in     \
	src/tse3logo.png.verbatim.in

###############################################################################
# These are the files that get built

HTML_FILES =        \
	About.html      \
	Article.html    \
	Build.html      \
	Bugs.html       \
	Commands.html   \
	Copyright.html  \
	Error.html      \
	Examples.html   \
	Feedback.html   \
	HOWTO.html      \
	History.html    \
	InsFiles.html   \
	KDOC.html       \
	Mutex.html      \
	Notifier.html   \
	Playable.html   \
	Porting.html    \
	Psalm150.html   \
	Song.html       \
	Structure.html  \
	TSE3MDL.html    \
	Trax.html       \
	Trouble.html    \
	Whitepaper.html \
	Version.html    \
	index.html

VERBATIM_FILES =   \
	History        \
	pete.jpeg      \
	trax.gif       \
	tse3.gif       \
	tse3logo.png


###############################################################################
# This is how they get built

HTMLIZE      = $(srcdir)/src/htmlize.pl
VERSION_FILE = $(top_srcdir)/Version
VERSION      = `cat $(VERSION_FILE)`

all-local: $(HTML_FILES) $(VERBATIM_FILES) $(HTMLIZE) $(VERSION_FILE)

clean-local:
	rm -rf *.html api

tse3-doxygen:
	@cd ../src; doxygen
tse3-kdoc:
	@cd ../src/tse3; make tse3-kdoc
tse3-kdoc-all:
	@cd ../src/tse3; make tse3-kdoc-all
tse3-kdoc-libs:
	@cd ../src/tse3; make tse3-kdoc-libs

%.html: src/%.html.in
	@echo "Creating $@ from $<"
	@if (which perl > /dev/null 2>/dev/null); then \
	perl $(HTMLIZE) $(VERSION) < $< > $@; \
	else cp $< $@; fi


%.gif: src/%.gif.verbatim.in
	@echo "Creating $@ from $<"
	cp $< $@
%.png: src/%.png.verbatim.in
	@echo "Creating $@ from $<"
	cp $< $@
%.jpeg: src/%.jpeg.verbatim.in
	@echo "Creating $@ from $<"
	cp $< $@


###############################################################################
# And this is how they are installed

if INSTALL_TSE3_DOC
docs_DATA = $(HTML_FILES) $(VERBATIM_FILES)
docsdir = ${prefix}/doc/${PACKAGE}-${VERSION}
endif

