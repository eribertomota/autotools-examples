
bin_PROGRAMS=missidentify

missidentify_SOURCES = main.c dig.c check.c helpers.c ui.c cycles.c \
                       main.h tchar-local.h

man_MANS=missidentify.1

EXTRA_DIST=$(man_MANS) config.guess config.sub sample.c sample.jpg

# ----------------------------------------------------------------------
# Packaging

WINDOWSDOCS=README.TXT NEWS.TXT USAGE.TXT

README.TXT: README
	cp README README.TXT

USAGE.TXT: $(man_MANS)
	man ./missidentify.1 | col -bx > USAGE.TXT

NEWS.TXT:NEWS
	cp NEWS NEWS.TXT

win-docs: $(WINDOWSDOCS)
	flip -d $(WINDOWSDOCS)
#       unix2dos $(WINDOWSDOCS)

win-package: win-docs
	rm -rf $(distdir).zip $(distdir)
	make
	$(STRIP) missidentify.exe
	mkdir $(distdir)
	cp $(WINDOWSDOCS) missidentify.exe sample.{c,jpg} $(distdir)
	zip -r9 $(distdir).zip $(distdir)
	rm -rf $(distdir) $(WINDOWSDOCS)

world: distclean
	./configure --host=mingw32
	make win-package
	make dist


# ----------------------------------------------------------------------
# Cleanup code

nice:
	rm -f *~

preflight:
	@grep RBF $(DISTFILES)


