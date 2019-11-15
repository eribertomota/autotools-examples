dnl $Id: configure.ac,v 1.52.2.1 2010/12/28 22:27:20 dan Exp $
dnl Process this file with autoconf to produce a configure script.
dnl
dnl Copyright (c) 2002, 2003, 2004, 2005, 2006, 2007, 2010 Dan McMahill
dnl All rights reserved.
dnl
dnl This code is derived from software written by Dan McMahill
dnl
dnl Redistribution and use in source and binary forms, with or without
dnl modification, are permitted provided that the following conditions
dnl are met:
dnl 1. Redistributions of source code must retain the above copyright
dnl    notice, this list of conditions and the following disclaimer.
dnl 2. Redistributions in binary form must reproduce the above copyright
dnl    notice, this list of conditions and the following disclaimer in the
dnl    documentation and/or other materials provided with the distribution.
dnl 3. All advertising materials mentioning features or use of this software
dnl    must display the following acknowledgement:
dnl        This product includes software developed by Dan McMahill
dnl  4. The name of the author may not be used to endorse or promote products
dnl     derived from this software without specific prior written permission.
dnl    
dnl  THIS SOFTWARE IS PROVIDED BY THE AUTHOR ``AS IS'' AND ANY EXPRESS OR
dnl  IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES
dnl  OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED.
dnl  IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY DIRECT, INDIRECT,
dnl  INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING,
dnl  BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
dnl  LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED
dnl  AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
dnl  OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY
dnl  OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF
dnl  SUCH DAMAGE.
dnl    

AC_INIT(latex.mk.in.in)
AM_INIT_AUTOMAKE(latex-mk, 2.1)

AM_MAINTAINER_MODE

#
# determine host type
#
AC_CANONICAL_HOST

#
# an install program
#
AC_PROG_INSTALL

#
# general
#
AC_PATH_PROG(AWK, awk nawk gawk mawk, awk)
AC_PATH_PROG(ENV_PROG, env, env)
AC_PATH_PROG(FALSE, false, false)
AC_PATH_PROG(GREP, grep, grep)
AC_PATH_PROG(GZCAT, gzcat, gzcat)
AC_PATH_PROG(GZIP, gzip, gzip)
AC_PATH_PROG(RM, rm, rm)
AC_PATH_PROG(RMDIR, rmdir, rmdir)
AC_PATH_PROG(TAR, tar, tar)

#
# for latex.mk
#
AC_PATH_PROG(BIBTEX, bibtex, bibtex)
# for converting graphics file formats (from ImageMagick)
AC_PATH_PROG(CONVERT, convert, convert)
AC_PATH_PROG(DVIPDFM, dvipdfm, dvipdfm)
AC_PATH_PROG(DVIPS, dvips, dvips)
AC_PATH_PROG(ECHO, echo, echo)
AC_PATH_PROG(FIND, find, find)
AC_PATH_PROG(GV, gv, gv)
AC_PATH_PROG(HEVEA, hevea, hevea)
AC_PATH_PROG(HACHA, hacha, hacha)
AC_PATH_PROG(IMAGEN, imagen, imagen)
AC_PATH_PROG(LATEX, latex, latex)
AC_PATH_PROG(LATEX2HTML, latex2html, latex2html)
AC_PATH_PROG(LATEX2RTF, latex2rtf, latex2rtf)
AC_PATH_PROG(LPR, lpr, lpr)
AC_PATH_PROG(MAKEIDX, makeindex, makeindex)
AC_PATH_PROG(PDFLATEX, pdflatex, pdflatex)
AC_PATH_PROG(PS2PDF, ps2pdf, ps2pdf)
AC_PATH_PROG(TEX2PAGE, tex2page, tex2page)
AC_PATH_PROG(XDVI, xdvi, xdvi)

#
# for lgrind.mk
#
AC_PATH_PROG(LGRIND, lgrind, lgrind)

#
# for mpost.mk
#
AC_PATH_PROG(MPOST, mpost mp, mpost)

#
# for tgif.mk
#
AC_PATH_PROG(TGIF, tgif, tgif)

#
# for xfig.mk
#
AC_PATH_PROG(FIG2DEV, fig2dev, fig2dev)

#
# Look for a GNU make program and a BSD make program
# This is used by the testsuite
#

AC_PATH_GNU_MAKE
AC_PATH_BSD_MAKE

if test "X${BMAKE}" = "Xnone" -a "X${GMAKE}" = "Xnone" ; then
	AC_MSG_NOTICE([

************************ WARNING ************************
I could not find GNU make >= version 3.80 _or_
a suitable BSD make on your system.  This package
will still install correctly, but you will not actually
be able to use it or run the testsuite until you 
install a suitable make program.
************************ WARNING ************************

]
)
fi

#
# system config files
#

AC_ARG_WITH([mkconf],
[  --with-mkconf=mkconf    Use the specified file as the site configuration
                          file for BSD make.  [default = /etc/latex-mk.conf]],
[
if test "X$with_mkconf" = "Xno" ; then
        AC_ERROR([--without-mkconf is not supported])
else
        MAKECONF="$with_mkconf"
fi
],
[
MAKECONF=@latexmkconfdir@/latex-mk.conf
])
AC_SUBST(MAKECONF)

AC_ARG_WITH([gmkconf],
[  --with-gmkconf=gmkconf  Use the specified file as the site configuration
                          file for GNU make.  [default = /etc/latex-gmk.conf]],
[
if test "X$with_gmkconf" = "Xno" ; then
        AC_ERROR([--without-gmkconf is not supported])
else
        GMAKECONF="$with_gmkconf"
fi
],
[
GMAKECONF=@latexmkconfdir@/latex-gmk.conf
])
AC_SUBST(GMAKECONF)


AC_ARG_WITH([usermkconf],
[  --with-mkconf=usermkconf
                          Use the specified file as the site configuration
                          file for BSD make.  [default = $HOME/.latex-mk.conf]],
[
if test "X$with_usermkconf" = "Xno" ; then
        AC_ERROR([--without-usermkconf is not supported])
else
        USERMAKECONF="$with_usermkconf"
fi
],
[
USERMAKECONF="\${HOME}/.latex-mk.conf"
])
AC_SUBST(USERMAKECONF)

AC_ARG_WITH([usergmkconf],
[  --with-usergmkconf=usergmkconf
                          Use the specified file as the user configuration
                          file for GNU make.  [default = $HOME/.latex-gmk.conf]],
[
if test "X$with_usergmkconf" = "Xno" ; then
        AC_ERROR([--without-usergmkconf is not supported])
else
        USERGMAKECONF="$with_usergmkconf"
fi
],
[
USERGMAKECONF="\${HOME}/.latex-gmk.conf"
])
AC_SUBST(USERGMAKECONF)


AC_OUTPUT(
	Makefile
	doc/Makefile
	doc/prefix.texi
	example/Makefile
	example/tgif/Makefile
	ieee-copyout
	latex-mk
	latex.mk.in
	latex.subdir.mk.in
	lgrind.mk.in
	mpost.mk.in
	testsuite/Makefile
	testsuite/bmake_ref/Makefile
	testsuite/gmake_ref/Makefile
	testsuite/latex_mk_ref/Makefile
	tgif.mk.in
	xfig.mk.in
)
