pkglibexecdir = ${libexecdir}/freepwing
pkgperllibdir = ${perllibdir}/FreePWING
fpwperllibdir = ${pkgperllibdir}/FPWUtils

bin_SCRIPTS = fpwmake
pkglibexec_SCRIPTS = fpwcgraph fpwcontrol fpwfullchar fpwhalfchar fpwindex \
	fpwlink fpwsort fpwsound cphier mkdirhier perl.sh
pkgdata_DATA = fpwutils.mk
fpwperllib_DATA = ColorGraphic.pm Copyright.pm FPWParser.pm FPWUtils.pm \
	KeyWord.pm Heading.pm Menu.pm Sound.pm Text.pm Word2.pm

EXTRA_DIST = $(fpwperllib_DATA) fpwmake.in fpwcgraph.in fpwcontrol.in \
	fpwfullchar.in fpwhalfchar.in fpwindex.in fpwlink.in fpwsort.in \
	fpwsound.in mkdirhier fpwutils.mk.in cphier.in perl.sh.in
CLEANFILES = fpwmake fpwcgraph fpwcontrol fpwfullchar fpwhalfchar fpwindex \
	fpwlink fpwsort fpwsound cphier perl.sh fpwutils.mk

fpwmake: fpwmake.in Makefile
	rm -f $@
	sed -e 's;\@GNUMAKE\@;$(GNUMAKE);' \
	   -e 's;\@pkgdatadir\@;$(pkgdatadir);' \
	   $(srcdir)/$@.in > $@.tmp
	cp $@.tmp $@
	chmod 755 $@
	rm -f $@.tmp

fpwcgraph: fpwcgraph.in Makefile
	rm -f $@
	sed -e 's;\@PERL\@;$(PERL);' $(srcdir)/$@.in > $@.tmp
	cp $@.tmp $@
	chmod 755 $@
	rm -f $@.tmp

fpwcontrol: fpwcontrol.in Makefile
	rm -f $@
	sed -e 's;\@PERL\@;$(PERL);' $(srcdir)/$@.in > $@.tmp
	cp $@.tmp $@
	chmod 755 $@
	rm -f $@.tmp

fpwfullchar: fpwfullchar.in Makefile
	rm -f $@
	sed -e 's;\@PERL\@;$(PERL);' $(srcdir)/$@.in > $@.tmp
	cp $@.tmp $@
	chmod 755 $@
	rm -f $@.tmp

fpwhalfchar: fpwhalfchar.in Makefile
	rm -f $@
	sed -e 's;\@PERL\@;$(PERL);' $(srcdir)/$@.in > $@.tmp
	cp $@.tmp $@
	chmod 755 $@
	rm -f $@.tmp

fpwindex: fpwindex.in Makefile
	rm -f $@
	sed -e 's;\@PERL\@;$(PERL);' $(srcdir)/$@.in > $@.tmp
	cp $@.tmp $@
	chmod 755 $@
	rm -f $@.tmp

fpwlink: fpwlink.in Makefile
	rm -f $@
	sed -e 's;\@PERL\@;$(PERL);' $(srcdir)/$@.in > $@.tmp
	cp $@.tmp $@
	chmod 755 $@
	rm -f $@.tmp

fpwsort: fpwsort.in Makefile
	rm -f $@
	sed -e 's;\@PERL\@;$(PERL);' $(srcdir)/$@.in > $@.tmp
	cp $@.tmp $@
	chmod 755 $@
	rm -f $@.tmp

fpwsound: fpwsound.in Makefile
	rm -f $@
	sed -e 's;\@PERL\@;$(PERL);' $(srcdir)/$@.in > $@.tmp
	cp $@.tmp $@
	chmod 755 $@
	rm -f $@.tmp

fpwutils.mk: fpwutils.mk.in Makefile
	rm -f $@
	sed -e 's;\@pkglibexecdir\@;$(pkglibexecdir);' \
	   -e 's;\@datadir\@;$(datadir);' \
	   $(srcdir)/$@.in > $@.tmp
	cp $@.tmp $@
	chmod 644 $@
	rm -f $@.tmp

cphier: cphier.in Makefile
	rm -f $@
	sed -e 's;\@pkglibexecdir\@;$(pkglibexecdir);' \
	   $(srcdir)/$@.in > $@.tmp
	cp $@.tmp $@
	chmod 755 $@
	rm -f $@.tmp

perl.sh: perl.sh.in Makefile
	rm -f $@
	sed -e 's;\@PERL\@;$(PERL);' \
	   $(srcdir)/$@.in > $@.tmp
	cp $@.tmp $@
	chmod 755 $@
	rm -f $@.tmp
