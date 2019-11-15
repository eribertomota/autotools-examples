AC_INIT([gkdebconf],
        [m4_esyscmd_s([dpkg-parsechangelog --show-field Version])])
AC_CONFIG_SRCDIR([src/main.c])
AM_INIT_AUTOMAKE
AC_CONFIG_HEADERS([config.h])

ALL_LINGUAS="pt_BR fr ja_JP sv cs ru de de_DE es es_ES pt"

AC_PROG_CC

AC_USE_SYSTEM_EXTENSIONS
AM_GNU_GETTEXT_VERSION([0.19])
AM_GNU_GETTEXT([external])

AC_HEADER_DIRENT
AC_HEADER_STDC

PKG_CHECK_MODULES([GKDEBCONF], [gtk+-3.0 >= 3.9.12], [],
                               [AC_MSG_ERROR([GTK 3 is required.])])
AC_SUBST([GKDEBCONF_CFLAGS])
AC_SUBST([GKDEBCONF_LIBS])

GLIB_GSETTINGS

##################################################
# Check for gtk-doc.
##################################################
                                                                                                                                           
AC_ARG_WITH(html-dir, [  --with-html-dir=PATH path to installed docs ])
                                                                                                                                           
if test "x$with_html_dir" = "x" ; then
  HTML_DIR='${datadir}/gtk-doc/html'
else
  HTML_DIR=$with_html_dir
fi
                                                                                                                                           
AC_SUBST(HTML_DIR)
                                                                                                                                           
PKG_CHECK_MODULES([GTKDOC], [gtk-doc >= 1.0], [GTKDOC=true], [GTKDOC=false])
                                                                                                                                           
dnl Let people disable the gtk-doc stuff.
AC_ARG_ENABLE(gtk-doc, [  --enable-gtk-doc  Use gtk-doc to build documentation [default=no]], enable_gtk_doc="$enableval", 
enable_gtk_doc=no)
                                                                                                                                           
AM_CONDITIONAL(ENABLE_GTK_DOC, test x$enable_gtk_doc = xyes)
AM_CONDITIONAL(GTK_DOC_USE_LIBTOOL, test x$use_libtool = xyes)
# end of gtk-doc check

                                                                                                                                           
AC_CONFIG_FILES([
	Makefile
	po/Makefile.in
	src/Makefile
	scripts/Makefile
	pixmaps/Makefile
	man/Makefile
	docs/Makefile
])
AC_OUTPUT

