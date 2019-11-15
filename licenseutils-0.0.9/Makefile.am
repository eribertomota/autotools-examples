# Copyright (C) 2013 Ben Asselstine
# 
# Copying and distribution of this file, with or without modification,
# are permitted in any medium without royalty provided the copyright
# notice and this notice are preserved.  This file is offered as-is,
# without any warranty.
ACLOCAL_AMFLAGS = -I lib/m4 -I m4 
SUBDIRS=lib lang-files src po tests doc
EXTRA_DIST = bootstrap bootstrap.conf TODO build-aux/config.rpath \
	     HACKING completion/licensing-completion.bash lu-sh.1 notice.1 styles.ac lu-comment-extractor.1

if USE_BASH_COMPLETION
  bash_completion_DATA = completion/licensing-completion.bash
else
  bash_completion_DATA = 
endif

# the following makery is to facilitate the creation of a tarball
# that can be built using the ./bootstrap command.
PREBOOTSTRAPFILES=\
$(srcdir)/configure.ac \
$(srcdir)/styles.ac \
$(srcdir)/Makefile.am \
$(srcdir)/bootstrap \
$(srcdir)/bootstrap.conf \
$(srcdir)/README \
$(srcdir)/AUTHORS \
$(srcdir)/COPYING \
$(srcdir)/NEWS \
$(srcdir)/TODO \
$(srcdir)/HACKING \
$(srcdir)/INSTALL \
$(srcdir)/ChangeLog \
$(srcdir)/lu-sh.1 \
$(srcdir)/notice.1 \
$(srcdir)/po/POTFILES.in \
$(srcdir)/po/LINGUAS \
$(srcdir)/doc/Makefile.am \
$(srcdir)/doc/licenseutils.texi \
$(srcdir)/doc/version.texi.in \
$(srcdir)/doc/gendocs \
$(srcdir)/completion/licensing-completion.bash \
$(srcdir)/src/Makefile.am \
$(srcdir)/src/styles.am \
$(srcdir)/src/licensing.c      $(srcdir)/src/licensing.h \
$(srcdir)/src/licensing_priv.h \
$(srcdir)/src/gettext-more.h \
$(srcdir)/src/util.h            $(srcdir)/src/util.c \
$(srcdir)/src/gpl.c             $(srcdir)/src/gpl.h \
$(srcdir)/src/lgpl.c            $(srcdir)/src/lgpl.h \
$(srcdir)/src/agpl.c            $(srcdir)/src/agpl.h \
$(srcdir)/src/fdl.c             $(srcdir)/src/fdl.h \
$(srcdir)/src/help.c            $(srcdir)/src/help.h \
$(srcdir)/src/welcome.c         $(srcdir)/src/welcome.h \
$(srcdir)/src/warranty.c        $(srcdir)/src/warranty.h \
$(srcdir)/src/boilerplate.c     $(srcdir)/src/boilerplate.h \
$(srcdir)/src/copyright.c       $(srcdir)/src/copyright.h \
$(srcdir)/src/cbb.c             $(srcdir)/src/cbb.h \
$(srcdir)/src/comment.c         $(srcdir)/src/comment.h \
$(srcdir)/src/uncomment.c       $(srcdir)/src/uncomment.h \
$(srcdir)/src/opts.c            $(srcdir)/src/opts.h \
$(srcdir)/src/choose.c          $(srcdir)/src/choose.h \
$(srcdir)/src/top.c             $(srcdir)/src/top.h \
$(srcdir)/src/project.c         $(srcdir)/src/project.h \
$(srcdir)/src/extra.c           $(srcdir)/src/extra.h \
$(srcdir)/src/all-permissive.c  $(srcdir)/src/all-permissive.h \
$(srcdir)/src/fsf-permissive.c  $(srcdir)/src/fsf-permissive.h \
$(srcdir)/src/png-boilerplate.c $(srcdir)/src/png-boilerplate.h \
$(srcdir)/src/png-apply.c       $(srcdir)/src/png-apply.h \
$(srcdir)/src/bsd.c             $(srcdir)/src/bsd.h \
$(srcdir)/src/mit.c             $(srcdir)/src/mit.h \
$(srcdir)/src/eclipse.c         $(srcdir)/src/eclipse.h \
$(srcdir)/src/zlib.c            $(srcdir)/src/zlib.h \
$(srcdir)/src/isc.c             $(srcdir)/src/isc.h \
$(srcdir)/src/mozilla.c         $(srcdir)/src/mozilla.h \
$(srcdir)/src/artistic.c        $(srcdir)/src/artistic.h \
$(srcdir)/src/apache.c          $(srcdir)/src/apache.h \
$(srcdir)/src/apply.c           $(srcdir)/src/apply.h \
$(srcdir)/src/prepend.c         $(srcdir)/src/prepend.h \
$(srcdir)/src/c-style.c         $(srcdir)/src/c-style.h \
$(srcdir)/src/c++-style.c       $(srcdir)/src/c++-style.h \
$(srcdir)/src/fortran-style.c   $(srcdir)/src/fortran-style.h \
$(srcdir)/src/pascal-style.c    $(srcdir)/src/pascal-style.h \
$(srcdir)/src/gettext-style.c   $(srcdir)/src/gettext-style.h \
$(srcdir)/src/groff-style.c     $(srcdir)/src/groff-style.h \
$(srcdir)/src/haskell-style.c   $(srcdir)/src/haskell-style.h \
$(srcdir)/src/m4-style.c        $(srcdir)/src/m4-style.h \
$(srcdir)/src/scheme-style.c    $(srcdir)/src/scheme-style.h \
$(srcdir)/src/shell-style.c     $(srcdir)/src/shell-style.h \
$(srcdir)/src/latex-style.c     $(srcdir)/src/latex-style.h \
$(srcdir)/src/texinfo-style.c   $(srcdir)/src/texinfo-style.h \
$(srcdir)/src/styles.c          $(srcdir)/src/styles.h \
$(srcdir)/src/new-boilerplate.c $(srcdir)/src/new-boilerplate.h \
$(srcdir)/src/preview.c         $(srcdir)/src/preview.h \
$(srcdir)/src/detect.c          $(srcdir)/src/detect.h \
$(srcdir)/src/forget.c          $(srcdir)/src/forget.h \
$(srcdir)/src/fsf-addresses.c   $(srcdir)/src/fsf-addresses.h \
$(srcdir)/src/url-downloader.c  $(srcdir)/src/url-downloader.h \
$(srcdir)/src/comment-style.h \
$(srcdir)/src/comment-extractor.cpp \
$(srcdir)/src/main.c \
$(srcdir)/src/lu-sh.in \
$(srcdir)/src/notice.in \
$(srcdir)/tests/Makefile.am \
$(srcdir)/tests/boilerplate/Makefile.am \
$(srcdir)/tests/boilerplate/0001 \
$(srcdir)/tests/boilerplate/0002 \
$(srcdir)/tests/boilerplate/0003 \
$(srcdir)/tests/boilerplate/0004 \
$(srcdir)/tests/boilerplate/0005 \
$(srcdir)/tests/boilerplate/0006 \
$(srcdir)/tests/cbb/Makefile.am \
$(srcdir)/tests/cbb/0001 \
$(srcdir)/tests/choose/Makefile.am \
$(srcdir)/tests/choose/0001 \
$(srcdir)/tests/choose/0002 \
$(srcdir)/tests/comment/Makefile.am \
$(srcdir)/tests/comment/0001 \
$(srcdir)/tests/copyright/Makefile.am \
$(srcdir)/tests/copyright/0001 \
$(srcdir)/tests/extra/Makefile.am \
$(srcdir)/tests/extra/0001 \
$(srcdir)/tests/png-apply/Makefile.am \
$(srcdir)/tests/png-apply/0001 \
$(srcdir)/tests/png-apply/0001.png \
$(srcdir)/tests/prepend/Makefile.am \
$(srcdir)/tests/prepend/0001 \
$(srcdir)/tests/prepend/0002 \
$(srcdir)/tests/prepend/0003 \
$(srcdir)/tests/prepend/0004 \
$(srcdir)/tests/prepend/0005 \
$(srcdir)/tests/preview/Makefile.am \
$(srcdir)/tests/preview/0001 \
$(srcdir)/tests/project/Makefile.am \
$(srcdir)/tests/project/0001 \
$(srcdir)/tests/top/Makefile.am \
$(srcdir)/tests/top/0001 \
$(srcdir)/tests/uncomment/Makefile.am \
$(srcdir)/tests/uncomment/0001 \
$(srcdir)/tests/uncomment/0002 \
$(srcdir)/tests/uncomment/0003 \
$(srcdir)/tests/uncomment/0004 \
$(srcdir)/lang-files/ada.lang \
$(srcdir)/lang-files/applescript.lang \
$(srcdir)/lang-files/asm.lang \
$(srcdir)/lang-files/awk.lang \
$(srcdir)/lang-files/bat.lang \
$(srcdir)/lang-files/bib.lang \
$(srcdir)/lang-files/bison.lang \
$(srcdir)/lang-files/caml.lang \
$(srcdir)/lang-files/c_comment.lang \
$(srcdir)/lang-files/changelog.lang \
$(srcdir)/lang-files/c.lang \
$(srcdir)/lang-files/clike_vardeclaration.lang \
$(srcdir)/lang-files/clipper.lang \
$(srcdir)/lang-files/cobol.lang \
$(srcdir)/lang-files/coffeescript.lang \
$(srcdir)/lang-files/conf.lang \
$(srcdir)/lang-files/cpp2html.css \
$(srcdir)/lang-files/cpp.lang \
$(srcdir)/lang-files/csharp.lang \
$(srcdir)/lang-files/css_common.outlang \
$(srcdir)/lang-files/css.lang \
$(srcdir)/lang-files/c_string.lang \
$(srcdir)/lang-files/default.css \
$(srcdir)/lang-files/default.lang \
$(srcdir)/lang-files/default.style \
$(srcdir)/lang-files/desktop.lang \
$(srcdir)/lang-files/diff.lang \
$(srcdir)/lang-files/d.lang \
$(srcdir)/lang-files/docbook.outlang \
$(srcdir)/lang-files/erlang.lang \
$(srcdir)/lang-files/errors.lang \
$(srcdir)/lang-files/esc256.outlang \
$(srcdir)/lang-files/esc256.style \
$(srcdir)/lang-files/esc.outlang \
$(srcdir)/lang-files/esc.style \
$(srcdir)/lang-files/extreme_comment2.lang \
$(srcdir)/lang-files/extreme_comment3.lang \
$(srcdir)/lang-files/extreme_comment.lang \
$(srcdir)/lang-files/feature.lang \
$(srcdir)/lang-files/fixed-fortran.lang \
$(srcdir)/lang-files/flex.lang \
$(srcdir)/lang-files/fortran.lang \
$(srcdir)/lang-files/function.lang \
$(srcdir)/lang-files/glsl.lang \
$(srcdir)/lang-files/go.lang \
$(srcdir)/lang-files/groff_man.outlang \
$(srcdir)/lang-files/groff_mm_color.outlang \
$(srcdir)/lang-files/groff_mm.outlang \
$(srcdir)/lang-files/groovy.lang \
$(srcdir)/lang-files/haskell.lang \
$(srcdir)/lang-files/haskell_literate.lang \
$(srcdir)/lang-files/haxe.lang \
$(srcdir)/lang-files/Hello2.css \
$(srcdir)/lang-files/Hello.css \
$(srcdir)/lang-files/html5_common.outlang \
$(srcdir)/lang-files/html5.outlang \
$(srcdir)/lang-files/html_common.outlang \
$(srcdir)/lang-files/htmlcss.outlang \
$(srcdir)/lang-files/html.lang \
$(srcdir)/lang-files/html_notfixed.outlang \
$(srcdir)/lang-files/html.outlang \
$(srcdir)/lang-files/html_ref.outlang \
$(srcdir)/lang-files/html_simple.lang \
$(srcdir)/lang-files/htmltablelinenum.outlang \
$(srcdir)/lang-files/htmltable.outlang \
$(srcdir)/lang-files/islisp.lang \
$(srcdir)/lang-files/javadoc.outlang \
$(srcdir)/lang-files/java.lang \
$(srcdir)/lang-files/javalog.lang \
$(srcdir)/lang-files/javalog.style \
$(srcdir)/lang-files/javascript.lang \
$(srcdir)/lang-files/json.lang \
$(srcdir)/lang-files/json.style \
$(srcdir)/lang-files/key_string.lang \
$(srcdir)/lang-files/langdef.lang \
$(srcdir)/lang-files/lang.map \
$(srcdir)/lang-files/latexcolor.outlang \
$(srcdir)/lang-files/latex.lang \
$(srcdir)/lang-files/latex.outlang \
$(srcdir)/lang-files/ldap.lang \
$(srcdir)/lang-files/lilypond.lang \
$(srcdir)/lang-files/lilypond.style \
$(srcdir)/lang-files/lisp.lang \
$(srcdir)/lang-files/log.lang \
$(srcdir)/lang-files/logtalk.lang \
$(srcdir)/lang-files/lsm.lang \
$(srcdir)/lang-files/lua.lang \
$(srcdir)/lang-files/m4.lang \
$(srcdir)/lang-files/makefile.lang \
$(srcdir)/lang-files/manifest.lang \
$(srcdir)/lang-files/mediawiki.outlang \
$(srcdir)/lang-files/mono-alt.css \
$(srcdir)/lang-files/mono.css \
$(srcdir)/lang-files/nohilite.lang \
$(srcdir)/lang-files/number.lang \
$(srcdir)/lang-files/odf.outlang \
$(srcdir)/lang-files/opa.lang \
$(srcdir)/lang-files/outlang.lang \
$(srcdir)/lang-files/outlang.map \
$(srcdir)/lang-files/oz.lang \
$(srcdir)/lang-files/pascal.lang \
$(srcdir)/lang-files/pc.lang \
$(srcdir)/lang-files/perl.lang \
$(srcdir)/lang-files/php.lang \
$(srcdir)/lang-files/po.lang \
$(srcdir)/lang-files/postscript.lang \
$(srcdir)/lang-files/prolog.lang \
$(srcdir)/lang-files/properties.lang \
$(srcdir)/lang-files/proto.lang \
$(srcdir)/lang-files/python.lang \
$(srcdir)/lang-files/r.lang \
$(srcdir)/lang-files/r.style \
$(srcdir)/lang-files/ruby.lang \
$(srcdir)/lang-files/scala.lang \
$(srcdir)/lang-files/scheme.lang \
$(srcdir)/lang-files/script_comment.lang \
$(srcdir)/lang-files/sexp.outlang \
$(srcdir)/lang-files/sh_acid.css \
$(srcdir)/lang-files/sh_berries-dark.css \
$(srcdir)/lang-files/sh_berries-light.css \
$(srcdir)/lang-files/sh_bipolar.css \
$(srcdir)/lang-files/sh_blacknblue.css \
$(srcdir)/lang-files/sh_bright.css \
$(srcdir)/lang-files/sh_contrast.css \
$(srcdir)/lang-files/sh_darkblue.css \
$(srcdir)/lang-files/sh_darkness.css \
$(srcdir)/lang-files/sh_desert.css \
$(srcdir)/lang-files/sh_dull.css \
$(srcdir)/lang-files/sh_easter.css \
$(srcdir)/lang-files/sh_emacs.css \
$(srcdir)/lang-files/sh_golden.css \
$(srcdir)/lang-files/sh_greenlcd.css \
$(srcdir)/lang-files/sh_ide-anjuta.css \
$(srcdir)/lang-files/sh_ide-codewarrior.css \
$(srcdir)/lang-files/sh_ide-devcpp.css \
$(srcdir)/lang-files/sh_ide-eclipse.css \
$(srcdir)/lang-files/sh_ide-kdev.css \
$(srcdir)/lang-files/sh_ide-msvcpp.css \
$(srcdir)/lang-files/sh_kwrite.css \
$(srcdir)/lang-files/sh.lang \
$(srcdir)/lang-files/sh_matlab.css \
$(srcdir)/lang-files/sh_navy.css \
$(srcdir)/lang-files/sh_nedit.css \
$(srcdir)/lang-files/sh_neon.css \
$(srcdir)/lang-files/sh_night.css \
$(srcdir)/lang-files/sh_pablo.css \
$(srcdir)/lang-files/sh_peachpuff.css \
$(srcdir)/lang-files/sh_print.css \
$(srcdir)/lang-files/sh_rand01.css \
$(srcdir)/lang-files/sh_the.css \
$(srcdir)/lang-files/sh_typical.css \
$(srcdir)/lang-files/sh_vampire.css \
$(srcdir)/lang-files/sh_vim.css \
$(srcdir)/lang-files/sh_vim-dark.css \
$(srcdir)/lang-files/sh_whatis.css \
$(srcdir)/lang-files/sh_whitengrey.css \
$(srcdir)/lang-files/sh_zellner.css \
$(srcdir)/lang-files/s.lang \
$(srcdir)/lang-files/slang.lang \
$(srcdir)/lang-files/sml.lang \
$(srcdir)/lang-files/spec.lang \
$(srcdir)/lang-files/sql.lang \
$(srcdir)/lang-files/style2.style \
$(srcdir)/lang-files/style3.style \
$(srcdir)/lang-files/style.defaults \
$(srcdir)/lang-files/style.lang \
$(srcdir)/lang-files/symbols.lang \
$(srcdir)/lang-files/tcl.lang \
$(srcdir)/lang-files/texinfo.lang \
$(srcdir)/lang-files/texinfo.outlang \
$(srcdir)/lang-files/texinfo.style \
$(srcdir)/lang-files/tml_formatting_all.lang \
$(srcdir)/lang-files/tml_formatting.lang \
$(srcdir)/lang-files/tml_glue.lang \
$(srcdir)/lang-files/tml.lang \
$(srcdir)/lang-files/tml_macrolinks.lang \
$(srcdir)/lang-files/tml_macros1.lang \
$(srcdir)/lang-files/tml_macros2.lang \
$(srcdir)/lang-files/tml_macrosdelayed1.lang \
$(srcdir)/lang-files/tml_macrosdelayed2.lang \
$(srcdir)/lang-files/tml_macrosdelayed3.lang \
$(srcdir)/lang-files/tml_macros.lang \
$(srcdir)/lang-files/tml_macrotokens.lang \
$(srcdir)/lang-files/todo.lang \
$(srcdir)/lang-files/upc.lang \
$(srcdir)/lang-files/url.lang \
$(srcdir)/lang-files/vala.lang \
$(srcdir)/lang-files/vbscript.lang \
$(srcdir)/lang-files/xhtml_common.outlang \
$(srcdir)/lang-files/xhtml.css \
$(srcdir)/lang-files/xhtmlcss.outlang \
$(srcdir)/lang-files/xhtml_notfixed.outlang \
$(srcdir)/lang-files/xhtml.outlang \
$(srcdir)/lang-files/xhtmltable.outlang \
$(srcdir)/lang-files/xml.lang \
$(srcdir)/lang-files/xorg.lang \
$(srcdir)/lang-files/zsh.lang

manifest:
	@echo ${PREBOOTSTRAPFILES}

predist:
	make srcdir="`eval basename ${PWD}`" --silent -f ${PWD}/Makefile manifest > ${builddir}/.manifest
	rm -f ${PACKAGE}.tar.gz 2>/dev/null ;\
	tar --dereference --directory=.. -zcvf ${PACKAGE}.tar.gz `cat ${builddir}/.manifest` && rm ${builddir}/.manifest

CLEANFILES=.manifest licensing.1

#this chunk of makery is about getting a man page to build,
#despite a horribly broken help2man, and a non-standard --help in licensing.
man1_MANS=licensing.1 lu-sh.1 notice.1 lu-comment-extractor.1

licensing.1: $(builddir)/src/licensing
	$(HELP2MAN) --output=$(builddir)/$@ --name='a program for adding license notices to files' --source licenseutils --libtool  $(builddir)/src/licensing


