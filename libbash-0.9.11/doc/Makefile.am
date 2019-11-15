AUTOMAKE_OPTIONS = -Wno-portability

.PHONY: all clean

EXTRA_DIST = $(wildcard *.dox) $(wildcard *.in) 

# Adding `-' to make rules in order to ignore errors
clean:
	rm -rf html 

distclean: clean
	rm -rf Doxyfile main_page.dox Makefile

all: Doxyfile main_page.dox docs

# Old of versions of doxygen do not generate html correctly, if
# html dir already contains output of previous run.
# That's why we delete it first.
docs: clean 
	$(DOXYGEN)
	
install: all
	test X"$(DOXYGEN)" = "X" || \
	install -d $(DESTDIR)$(datadir)/doc/$(PACKAGE)
	test X"$(DOXYGEN)" = "X" || \
	cp -rf html $(DESTDIR)$(datadir)/doc/$(PACKAGE)
	
