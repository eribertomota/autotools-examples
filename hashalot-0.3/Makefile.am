
sbin_PROGRAMS = hashalot

man_MANS = hashalot.1

hashalot_SOURCES = hashalot.c rmd160.c rmd160.h sha512.c sha512.h

install-exec-hook:
	cd $(DESTDIR)$(sbindir) && \
	$(LN_S) -f hashalot$(EXEEXT) rmd160$(EXEEXT) && \
	$(LN_S) -f hashalot$(EXEEXT) sha256$(EXEEXT) && \
	$(LN_S) -f hashalot$(EXEEXT) sha384$(EXEEXT) && \
	$(LN_S) -f hashalot$(EXEEXT) sha512$(EXEEXT)

uninstall-hook:
	cd $(DESTDIR)$(sbindir) && \
	rm -f rmd160 sha256 sha384 sha512

TESTS = check.sh

