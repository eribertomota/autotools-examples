## $Id: Makefile.am,v 1.14 2006/06/07 17:56:48 dan Exp $
##
## Copyright (c) 2002, 2003, 2004, 2006 Dan McMahill
## All rights reserved.
##
## Redistribution and use in source and binary forms, with or without
## modification, are permitted provided that the following conditions
## are met:
## 1. Redistributions of source code must retain the above copyright
##    notice, this list of conditions and the following disclaimer.
## 2. Redistributions in binary form must reproduce the above copyright
##    notice, this list of conditions and the following disclaimer in the
##    documentation and/or other materials provided with the distribution.
## 3. All advertising materials mentioning features or use of this software
##    must display the following acknowledgement:
##        This product includes software developed by Dan McMahill
##  4. The name of the author may not be used to endorse or promote products
##     derived from this software without specific prior written permission.
## 
##  THIS SOFTWARE IS PROVIDED BY THE AUTHOR ``AS IS'' AND ANY EXPRESS OR
##  IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES
##  OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED.
##  IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY DIRECT, INDIRECT,
##  INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING,
##  BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
##  LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED
##  AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
##  OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY
##  OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF
##  SUCH DAMAGE.
##


MKSRCS=	mkfile.in
EXFILES= \
	biblio.tex \
	example.tex \
	ex2.tex \
	ex3.tex \
	ex4.bib \
	ex4.tex \
	ex5.tex \
	refs.bib 

BMKFILES=	${MKSRCS:.in=.mk}
GMKFILES=	${MKSRCS:.in=.gmk}

pkgexampledir=		${pkgdatadir}/example
pkgexample_DATA=	${BMKFILES} ${GMKFILES} ${EXFILES} README-example.txt

EXTRA_DIST=	${EXFILES} mkfile.in README-example.txt

DISTCLEANFILES=	\
	${BMKFILES} \
	${GMKFILES} \
	example.conf

SUBDIRS=	tgif

SUFFIXES=	.in .mk .gmk

SED_COMMON=	-e 's;@latexmkdatadir@;$(pkgdatadir);g' \
	-e 's;@latexmkconfdir@;${sysconfdir};g' \
	-e 's;@latexmkbindir@;${bindir};g' \
	-e '/^MAKECONF/d'

SED_COMMON_TEST=	-e 's;@latexmkdatadir@;$(top_srcdir);g' \
	-e 's;@latexmkconfdir@;${sysconfdir};g' \
	-e 's;@latexmkbindir@;${top_srcdir};g' 

.in.mk:
	sed -e 's/^BMK://g' -e '/^GMK:/d' ${SED_COMMON} $<  > $@

.in.gmk:
	sed -e 's/^GMK://g' -e '/^BMK:/d' ${SED_COMMON} $<  > $@

