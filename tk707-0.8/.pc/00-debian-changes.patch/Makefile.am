## process this file with automake to produce Makefile.in
#
#    This file is part of tk707.
#
#    Copyright (C) 2000, 2001, 2002, 2003, 2004 Chris Willing and Pierre Saramito 
#
#    tk707 is free software; you can redistribute it and/or modify
#    it under the terms of the GNU General Public License as published by
#    the Free Software Foundation; either version 2 of the License, or
#    (at your option) any later version.
#
#    Foobar is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU General Public License for more details.
#
#    You should have received a copy of the GNU General Public License
#    along with Foobar; if not, write to the Free Software
#    Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA  02111-1307  USA
#
# -----------------------------------------------------------------------------
# documentation
# -----------------------------------------------------------------------------

info_TEXINFOS = tk707.texi
htmldir       = ${datadir}/html
html_DATA     = tk707.html
man_MANS      = tk707.1

# -----------------------------------------------------------------------------
# the file set
# -----------------------------------------------------------------------------

noinst_PROGRAMS   = tcl2c tk707bin tk707tcl texi2help
tk707bin_SOURCES  = util707.c util707.h element707.c play.c \
		    tk707AppInit.c title_defs.c score_defs.c defsa.c ports.c \
		    title.c score.c gui.c procs.c help.c tk707.c nix_bit.h
tk707tcl_SOURCES  = util707.c util707.h element707.c playa.c \
		    tk707AppInit.c nix_bit.h \
		    defsa.c ports.c score.c score_defs.c gui.c title.c title_defs.c procs.c help.c tk707.c 

tcl2c_SOURCES     = tcl2c.c 
texi2help_SOURCES = texi2help.l 

tk707bin_LDFLAGS  = $(ALSA_LIBS)   $(TCLTK_LIBS)   $(X_LIBS)
tk707tcl_LDFLAGS  = $(ALSA_LIBS)   $(TCLTK_LIBS)   $(X_LIBS)
INCLUDES          = $(ALSA_CFLAGS) $(TCLTK_CFLAGS) $(X_CFLAGS)

pkgdata_DATA      = 707.map 727.map 7b7.map 7c7.map \
		    demo.dat son-montuno.dat carioca.dat \
		    tk707.help

TESTS             = check.sh
TESTS_ENVIRONMENT = MIDIDUMP=$(MIDIDUMP); export MIDIDUMP; /bin/sh

BUILT_SOURCES = \
	title.tcl title_defs.tcl \
	title.c   title_defs.c  \
	score.tcl score_defs.tcl \
	score.c   score_defs.c   \
	defs.c  ports.c gui.c procs.c help.c tk707.c \
	defsa.c playa.c

EXTRA_DIST = VERSION INSTALL texi2help.c \
	tk707.sh.in defs.tcl ports.tcl gui.tcl procs.tcl help.tcl \
	tk707.tcl \
	score.fig score_fig2tcl.sh \
	title.fig title_fig2tcl.sh \
	test_02.dat test_05.dat test_06.dat tst_scale.dat \
	son-montuno.dat \
	$(man_MANS) \
	$(BUILT_SOURCES) \
	tk707.html \
	go $(pkgdata_DATA) $(TESTS) \
	binaire-tk.valid-dump triolet-tk.valid-dump tst_scale.valid-dump \
	INSTALL.texi gpl.texi BUGS bootstrap depcomp

CLEANFILES = tk707.sh *.o *.mid *.bak *.dvi *.ps *.log

CVSIGNORE = 								\
	Makefile.in configure aclocal.m4 config.h.in stamp-h.in		\
	stamp-vti score_defs.tcl score_defs.c score.tcl score.c		\
	title_defs.tcl title_defs.c title.tcl title.c defsa.c		\
	defs.c ports.c procs.c help.c gui.c tk707.c playa.c INSTALL 	\
	version.texi texi2help.c tk707.help tk707.html			\
	$(srcdir)/Makefile.in $(srcdir)/configure

WCIGNORE = 								\
	COPYING VERSION binaire-tk.valid-dump gpl.texi install-sh	\
	mdate-sh missing mkinstalldirs tcl2c.c son-montuno.dat		\
	demo.dat test_02.dat test_05.dat test_06.dat texinfo.tex 	\
	score.fig title.fig triolet-tk.valid-dump tst_scale.dat 	\
	tst_scale.valid-dump depcomp

# -----------------------------------------------------------------------------
# specific rules to generate figure *.tcl from *.fig (requieres fig2dev)
# -----------------------------------------------------------------------------

title.tcl title_defs.tcl: title.fig title_fig2tcl.sh
	sh $(srcdir)/title_fig2tcl.sh $(srcdir)/title.fig

score.tcl score_defs.tcl: score.fig score_fig2tcl.sh
	sh $(srcdir)/score_fig2tcl.sh $(srcdir)/score.fig

# -----------------------------------------------------------------------------
# specific rules for documentation: html and INSTALL
# -----------------------------------------------------------------------------

tk707.info tk707.dvi tk707.html: tk707.texi INSTALL.texi

$(srcdir)/tk707.html: tk707.texi
	@if test x"${TEXI2HTML}" != x"" && test x"`echo ${TEXI2HTML} | grep missing`" = x""; then \
	     echo "$(TEXI2HTML) -monolithic ${srcdir}/tk707.texi"; 		\
	     $(TEXI2HTML) -monolithic ${srcdir}/tk707.texi; 			\
	    if test "${srcdir}" != "."; then 					\
		 echo "mv tk707.html ${srcdir}/tk707.html"; 			\
		 mv tk707.html ${srcdir}/tk707.html; 				\
	    fi;									\
	else 									\
	     true; 								\
	fi

all-local: INSTALL.txt

$(srcdir)/INSTALL.txt: INSTALL.texi
	if test x"${MAKEINFO}" != x"" && test x"`echo ${MAKEINFO} | grep missing`" = x""; then  \
		tmp_texi=INSTALL-tmp$$$$.texi ; 	\
		grep -v "@[a-z][a-z]index" $(srcdir)/INSTALL.texi | \
		    sed -e 's/^@node Installation,,, Top/@node Installation,,, (dir)/' \
		    > $$tmp_texi; \
		makeinfo -I . --no-header $$tmp_texi > INSTALL.txt; \
		/bin/rm -f $$tmp_texi;			\
		cp INSTALL.txt $(srcdir)/INSTALL; 	\
	else						\
		touch INSTALL.txt;			\
	fi

# -----------------------------------------------------------------------------
# specific rules for documentation: .help
# -----------------------------------------------------------------------------

$(srcdir)/tk707.help: tk707.texi texi2help
	./texi2help < $(srcdir)/tk707.texi > $(srcdir)/tk707.help

# -----------------------------------------------------------------------------
# specific install rule: local tk707bin becomes installed tk707bin
# -----------------------------------------------------------------------------

$(srcdir)/tk707.c: tk707.tcl tcl2c
	./tcl2c tcl_tk707 < $(srcdir)/tk707.tcl > $(srcdir)/tk707.c
$(srcdir)/ports.c: ports.tcl tcl2c
	./tcl2c tcl_ports < $(srcdir)/ports.tcl > $(srcdir)/ports.c
$(srcdir)/defs.c: defs.tcl tcl2c
	sed -e 's%set VERSION.*%set VERSION $(VERSION)%' < $(srcdir)/defs.tcl | ./tcl2c tcl_defs > $(srcdir)/defs.c
$(srcdir)/playa.c: play.c
	sed '1,8s%^$$%#define not_compile_tcl%' $(srcdir)/play.c > $(srcdir)/playa.c
$(srcdir)/defsa.c: defs.c
	sed 's%set PKGDATADIR.*%set PKGDATADIR $(pkgdatadir)%' $(srcdir)/defs.c > $(srcdir)/defsa.c
$(srcdir)/title.c: title.tcl tcl2c
	./tcl2c tcl_title < $(srcdir)/title.tcl > $(srcdir)/title.c
$(srcdir)/title_defs.c: title_defs.tcl tcl2c
	./tcl2c tcl_title_defs < $(srcdir)/title_defs.tcl > $(srcdir)/title_defs.c
$(srcdir)/score.c: score.tcl tcl2c
	./tcl2c tcl_score < $(srcdir)/score.tcl > $(srcdir)/score.c
$(srcdir)/score_defs.c: score_defs.tcl tcl2c
	./tcl2c tcl_score_defs < $(srcdir)/score_defs.tcl > $(srcdir)/score_defs.c
$(srcdir)/gui.c: gui.tcl tcl2c
	./tcl2c tcl_gui < $(srcdir)/gui.tcl > $(srcdir)/gui.c
$(srcdir)/procs.c: procs.tcl tcl2c
	./tcl2c tcl_procs < $(srcdir)/procs.tcl > $(srcdir)/procs.c
$(srcdir)/help.c: help.tcl tcl2c
	./tcl2c tcl_help < $(srcdir)/help.tcl > $(srcdir)/help.c

# -----------------------------------------------------------------------------
# specific rules for lex
# -----------------------------------------------------------------------------

$(srcdir)/texi2help.c: texi2help.l
	if test x"${LEX}" != x"" && test x"`echo ${LEX} | grep missing`" = x""; then \
	     echo "$(LEX) $(AM_LFLAGS) $(LFLAGS) ${srcdir}/texi2help.l && mv $(LEX_OUTPUT_ROOT).c $(srcdir)/texi2help.c"; \
	     $(LEX) $(AM_LFLAGS) $(LFLAGS) ${srcdir}/texi2help.l && mv $(LEX_OUTPUT_ROOT).c $(srcdir)/texi2help.c; \
	else \
	     test -f $(srcdir)/texi2help.c; \
	fi

# -----------------------------------------------------------------------------
# add to standard automake
# -----------------------------------------------------------------------------

install-exec-local: tk707bin tk707.sh
	$(mkinstalldirs) $(DESTDIR)$(bindir)
	sh $(srcdir)/install-sh -s -c tk707bin $(DESTDIR)$(bindir)/tk707bin
	$(INSTALL_SCRIPT) tk707.sh $(DESTDIR)$(bindir)/tk707

uninstall-local:
	/bin/rm -f $(DESTDIR)$(bindir)/tk707
	/bin/rm -f $(DESTDIR)$(bindir)/tk707bin

maintainer-clean-local:
	cd $(srcdir); /bin/rm -f ${BUILT_SOURCES} tk707.html tk707.help	\
		aclocal.m4 config.h config.log config.status		\
		configure INSTALL.txt Makefile Makefile.in stamp-h	\
		stamp-h.in stamp-vti texi2help.c tk707.help		\
		config.h.in tk707.info version.texi

# -----------------------------------------------------------------------------
# other rules
# -----------------------------------------------------------------------------

SUFFIXES = .mid .wav .mp3

.mid.wav:
	timidity $*.mid -Ow $*.wav
.wav.mp3:
	lame -b128 $*.wav $*.mp3

# optional cvs/automake environment
-include ${CVSMKROOT}/cvs.mk

