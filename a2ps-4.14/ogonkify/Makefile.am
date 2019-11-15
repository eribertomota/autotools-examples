# -*- Makefile -*-
#
## Process this file with automake to produce Makefile.in
## This seems to make problems with some makes
AUTOMAKE_OPTIONS = foreign
SUBDIRS = doc m4
ACLOCAL_AMFLAGS = -I m4
CLEANFILES = $(bin_SCRIPTS)

afmdir = $(pkgdatadir)/afm
fontsdir = $(pkgdatadir)/fonts
ogonkifydir = $(pkgdatadir)

SUFFIXES = .enc .ps .pfa .afm

encoding = ogonki
targetEncoding = adobe

ORIGINAL_ENCODINGS_AFMS = 						\
ascii.afm adobe.afm latin1.afm latin2.afm latin3.afm latin4.afm		\
latin5.afm latin6.afm latin7.afm latin9.afm cp1250.afm ogonki.afm	\
mac.afm ibmpc.afm hp.afm

ENCODINGS_VECTORS =	 						\
ascii.enc adobe.enc latin1.enc latin2.enc latin3.enc latin4.enc		\
latin5.enc latin6.enc latin7.enc latin9.enc cp1250.enc ogonki.enc	\
mac.enc ibmpc.enc hp.enc

ORIGINAL_AFMS =				\
pcrr.afm pcrro.afm pcrb.afm pcrbo.afm	\
ptmr.afm ptmri.afm ptmb.afm ptmbi.afm	\
phvr.afm phvro.afm phvb.afm phvbo.afm

ORIGINAL_COMP_FONTS_AFMS =			\
pcrr-c.afm pcrro-c.afm pcrb-c.afm pcrbo-c.afm	\
ptmr-c.afm ptmri-c.afm ptmb-c.afm ptmbi-c.afm	\
phvr-c.afm phvro-c.afm phvb-c.afm phvbo-c.afm

CREATED_AFMS =					\
pcrr-o.afm pcrro-o.afm pcrb-o.afm pcrbo-o.afm	\
ptmr-o.afm ptmri-o.afm ptmb-o.afm ptmbi-o.afm	\
phvr-o.afm phvro-o.afm phvb-o.afm phvbo-o.afm

CREATED_FONTS =					\
pcrr-o.ps pcrro-o.ps pcrb-o.ps pcrbo-o.ps	\
ptmr-o.ps ptmri-o.ps ptmb-o.ps ptmbi-o.ps	\
phvr-o.ps phvro-o.ps phvb-o.ps phvbo-o.ps

CREATED_PFAS =					\
pcrr-o.pfa pcrro-o.pfa pcrb-o.pfa pcrbo-o.pfa	\
ptmr-o.pfa ptmri-o.pfa ptmb-o.pfa ptmbi-o.pfa	\
phvr-o.pfa phvro-o.pfa phvb-o.pfa phvbo-o.pfa

PSPROGS = allchars.ps compose.ps helper.ps printenc.ps

#
# What gets installed
#

if EXTENSIONS
bin_SCRIPTS = ogonkify composeglyphs
ogonkify_DATA = $(ENCODINGS_VECTORS) $(CREATED_FONTS) $(PSPROGS) README
afm_DATA = $(CREATED_AFMS)
fonts_DATA = $(CREATED_PFAS)
endif


#
# The afm's and ps's for composite fonts
#
%-o.afm: ogonki.enc composeglyphs.in %-c.afm
	@fontname=`grep "$*	" $(srcdir)/fontname.dat	\
	  | sed 's/^.*	//'`; 				\
	echo "Working on $$fontname-Ogonki ($*-o)...";	\
	$(PERL) ./composeglyphs -i $*.afm -c $*-c.afm	\
	   -o $*-o.ps -n $$fontname-Ogonki		\
	   -a $*-o.afm -e ${encoding}.afm 		\
	   -t ${targetEncoding}.afm

%-o.ps: ogonki.enc composeglyphs.in %-c.afm
	@fontname=`grep "$*	" $(srcdir)/fontname.dat	\
	  | sed 's/^.*	//'`; 				\
	echo "Working on $$fontname-Ogonki ($*-o)...";	\
	$(PERL) ./composeglyphs -i $*.afm -c $*-c.afm	\
	   -o $*-o.ps -n $$fontname-Ogonki		\
	   -a $*-o.afm -e ${encoding}.afm 		\
	   -t ${targetEncoding}.afm

#
# We want to distribute the product of composeglyphs too, avoiding
# perl as a requirement
#
EXTRA_DIST = README VERSION						\
	adobe.enc ogonki.enc adobe.enc					\
	$(PSPROGS) fontname.dat						\
	$(ORIGINAL_ENCODINGS_AFMS) $(ORIGINAL_AFMS)			\
	$(ORIGINAL_COMP_FONTS_AFMS)					\
	$(CREATED_FONTS) $(CREATED_AFMS) $(ENCODINGS_VECTORS)

DISTCLEANFILES = $(CREATED_PFAS)

MAINTAINERCLEANFILES = $(CREATED_FONTS) $(CREATED_FONTS) $(CREATED_AFMS)

ogonkify: ogonkify.in
# Don't add $(srcdir) to ogonkify.in: it's built by configure
	sed -e "s#@LIBDIR@#$(ogonkifydir)#g" ogonkify.in > ogonkify-t
	chmod +x ogonkify-t
	mv ogonkify-t ogonkify

#
# Suffix rules
#
.afm.enc: composeglyphs.in
	@echo "Creating $* encoding vector..."
	$(PERL) ./composeglyphs -e $< -E $*.enc

.ps.pfa: ogonki.enc adobe.enc compose.ps
	@cat $(srcdir)/${encoding}.enc		\
	     $(srcdir)/${targetEncoding}.enc	\
	     $(srcdir)/compose.ps		\
	     $(srcdir)/$*.ps > $@.tmp 		\
	&& mv $@.tmp $@
