## Makefile for the sheets subdirectory of a2ps
## Copyright (c) 1995-2000 Akim Demaille, Miguel Santana

## Process this file with automake to produce Makefile.in

# The a2ps of this package
xa2ps = $(top_builddir)/src/a2ps
TAR = gtar

# As a new `feature' :), a2ps uses now even more directories
sheetsdir = $(pkgdatadir)/sheets

major_sheets = \
ada.ssh c.ssh card.ssh clisp.ssh cpp.ssh cxx.ssh eiffel.ssh elisp.ssh	\
for-fixed.ssh for-free.ssh for77-fixed.ssh for77-free.ssh		\
for77kwds.ssh for90-fixed.ssh for90-free.ssh for90kwds.ssh fortran.ssh	\
gnuc.ssh java.ssh mail.ssh make.ssh objc.ssh ocaml.ssh pascal.ssh	\
perl.ssh pre.ssh pretex.ssh scheme.ssh sh.ssh shell.ssh ssh.ssh		\
symbols.ssh tcl.ssh texscript.ssh tk.ssh udiff.ssh wdiff.ssh

minor_sheets = \
68000.ssh a2psrc.ssh asn1.ssh autoconf.ssh awk.ssh b.ssh bc.ssh		\
caml.ssh chlog.ssh cidl.ssh claire.ssh coqv.ssh csh.ssh csharp.ssh	\
dc_shell.ssh eps.ssh gmake.ssh haskell.ssh html.ssh idl.ssh initora.ssh	\
is5rul.ssh js.ssh lace.ssh lex.ssh lout.ssh maple.ssh matlab.ssh	\
matlab4.ssh mib.ssh mly.ssh modula2.ssh modula3.ssh nasm.ssh o2c.ssh	\
oberon.ssh octave.ssh oracle.ssh pic16f84.ssh plsql.ssh pov.ssh ppd.ssh	\
ps.ssh prolog.ssh promela.ssh python.ssh rexx.ssh sather.ssh sdl88.ssh	\
sed.ssh	small.ssh sml.ssh specc.ssh sql.ssh sql92.ssh stratego.ssh	\
tclx.ssh tcsh.ssh tex.ssh texinfo.ssh tiger.ssh unity.ssh vba.ssh 	\
verilog.ssh vhdl.ssh vrml.ssh vtcl.ssh yacc.ssh xs.ssh zsh.ssh		\
php.ssh rd.ssh s.ssh st.ssh ruby.ssh

if EXTENSIONS
sheets_DATA = sheets.map $(major_sheets) $(minor_sheets)
else
sheets_DATA = sheets.map $(major_sheets)
endif

EXTRA_DIST = sheets.map $(major_sheets) $(minor_sheets)

# An HTML page to present the currently known style sheets
sheets.html: sheets.tar.gz
	. $(top_builddir)/tests/defs && $(xa2ps) --list=html-style-sheets > $@-t
	chmod 644 $@-t
	mv $@-t $@
	@echo "To install these files, run"
	@echo "cp *.ssh sheets.map sheets.html sheets.tar.gz <destdir>"
	@echo "cp sheets.map <destdir>/sheets.mp"

# A tar.gz of the current style sheets
sheetsdist:	sheets.tar.gz

# Basic dependencies
sheets.tar.gz: Makefile.am
	distdir=/tmp/sheets ;\
	rm -rf $$distdir ; mkdir $$distdir ; \
	for file in *.ssh sheets.map; do \
	  test -f $$distdir/$$file \
	  || ln $$file $$distdir/$$file 2> /dev/null \
	  || cp -p $$file $$distdir/$$file; \
	done ;	\
	(cd /tmp ; \
	GZIP=$(GZIP) $(TAR) chozf $@ sheets) ;\
	rm -rf $$distdir
	mv /tmp/$@ .

# Check that all the sheets are included in the package.
check:
	rm -f check.t check.t1 check.t2
	for i in $(major_sheets) $(minor_sheets); do \
	  echo $$i >> check.t; \
	done
	sort check.t | uniq > check.t1
	rm -f check.t
	for i in `cd $(srcdir) && echo *.ssh`; do \
	  echo $$i >> check.t; \
	done
	sort check.t | uniq > check.t2
	if cmp check.t1 check.t2 >/dev/null; then :; else \
	  echo "There are differences between available style sheets"; \
	  echo "and distributed style sheets."; \
	  diff check.t1 check.t2; \
	fi
	rm -f check.t check.t1 check.t2
