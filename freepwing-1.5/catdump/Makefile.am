pkglibexecdir = ${libexecdir}/freepwing
catalogsdir = ${pkgdatadir}/catalogs

pkgdoc_DATA = catdump.txt
pkglibexec_SCRIPTS = catdump
catalogs_DATA = catalogs catalogs.txt

EXTRA_DIST = catdump.in catdump.txt catalogs catalogs.txt
CLEANFILES = catdump

catdump: catdump.in Makefile
	rm -f $@
	sed -e 's;\@PERL\@;$(PERL);' -e 's;\@VERSION\@;$(VERSION);' \
	    $(srcdir)/$@.in > $@.tmp
	cp $@.tmp $@
	chmod 755 $@
	rm -f $@.tmp
