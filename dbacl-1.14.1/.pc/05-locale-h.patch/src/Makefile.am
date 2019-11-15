# note . occurs before tests
SUBDIRS = . tests

bin_PROGRAMS = dbacl bayesol mailinspect hmine hypex 
bin_SCRIPTS = mailcross mailtoe mailfoot

PUBDOM = jenkins.c jenkins2.c \
	mconf.h mtherr.c igam.c gamma.c const.c polevl.c isnan.c ndtr.c

datarootdir ?= $(prefix)/share

dbacl_SOURCES = dbacl.c dbacl.h fram.c catfun.c fh.c util.c util.h probs.c $(PUBDOM)
dbacl_LDADD = mb.o wc.o
EXTRA_dbacl_SOURCES = mbw.h mbw.c splintrc lint-check.sh

bayesol_SOURCES = bayesol.c bayesol.h fram.c risk-lexer.l risk-parser.y risk-parser.h probs.c util.c util.h $(PUBDOM)
bayesol_LDADD = @LEXLIB@

mailinspect_SOURCES = mailinspect.c mailinspect.h dbacl.h fram.c fh.c catfun.c probs.c util.c util.h $(PUBDOM)
mailinspect_LDADD = mb.o wc.o $(LDADDINTER)
INCLUDES = $(INCLUDESINTER)
EXTRA_mailinspect_SOURCES = mbw.h mbw.c

hmine_SOURCES = hmine.c hmine.h hparse.c fram.c util.h util.c dbacl.h rfc822.c rfc2822.c $(PUBDOM)

hypex_SOURCES = hypex.c hypex.h dbacl.h fram.c catfun.c util.h util.c probs.c $(PUBDOM)

# stuff_SOURCES = stuff.c stuff.h fram.c stuff-lexer.l stuff-parser.y stuff-parser.h probs.c util.c util.h $(PUBDOM)
# stuff_LDADD = @LEXLIB@

AM_CFLAGS = -funsigned-char -std=c99 -Wall -pedantic $(CFLAGSIEEE) -O3
AM_YFLAGS = -d

CLEANFILES = mailcross mailtoe mailfoot 
EXTRA_DIST = README mailcross.in mailtoe.in mailfoot.in mailtest.functions.in plot-scores.sh

mb.o: mbw.c dbacl.h mbw.h
	$(COMPILE) -DMBW_MB -c $(srcdir)/mbw.c -o $@

wc.o: mbw.c dbacl.h mbw.h
	$(COMPILE) -DMBW_WIDE -c $(srcdir)/mbw.c -o $@

SUFFIXES = .in

.in:
	cat $< \
		| sed -e '/# begin mailtest.functions/r mailtest.functions.in' \
		| sed -e '/# begin mailtest/,/# begin mailtest/d;/# end/,/# end/d' \
		| sed -e "s|[@]VERSION@|$(VERSION)|g;s|[@]PKGDATADIR@|$(pkgdatadir)|g" \
		> $@
	chmod +x $@


check_PROGRAMS = icheck pcheck
icheck_SOURCES = icheck.c dbacl.h fram.c catfun.c util.c util.h fh.c probs.c $(PUBDOM)
icheck_LDADD = mb.o wc.o

pcheck_SOURCES = hparse.c
pcheck: hparse.c hmine.h dbacl.h rfc822.c rfc2822.c
	$(COMPILE) -DTEST_PARSER $(srcdir)/hparse.c $(srcdir)/rfc822.c $(srcdir)/rfc2822.c util.o fram.o jenkins2.o -o pcheck $(LDFLAGS)

lint-check:
	sh ./lint-check.sh
