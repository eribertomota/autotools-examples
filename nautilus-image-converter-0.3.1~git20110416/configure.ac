AC_INIT([nautilus-image-converter], [0.3.1], [j@bitron.ch], [nautilus-image-converter])
AC_CONFIG_MACRO_DIR([m4])
AC_CONFIG_SRCDIR([Makefile.am])
AC_CONFIG_HEADERS(config.h)
AM_INIT_AUTOMAKE([dist-bzip2])
m4_ifdef([AM_SILENT_RULES],[AM_SILENT_RULES([yes])])

AM_MAINTAINER_MODE

# Checks for programs.
AC_PROG_CC
AC_DISABLE_STATIC
IT_PROG_INTLTOOL([0.35.0])
AC_PROG_LIBTOOL
AC_PATH_PROG(PKG_CONFIG, pkg-config, no)

GNOME_COMPILE_WARNINGS([maximum])
GNOME_CXX_WARNINGS
GNOME_DEBUG_CHECK
GNOME_MAINTAINER_MODE_DEFINES

AH_TEMPLATE([GETTEXT_PACKAGE], [Package name for gettext])
GETTEXT_PACKAGE=nautilus-image-converter
AC_DEFINE_UNQUOTED(GETTEXT_PACKAGE, "$GETTEXT_PACKAGE")
AC_SUBST(GETTEXT_PACKAGE)
AM_GLIB_GNU_GETTEXT

AC_SUBST(CFLAGS)
AC_SUBST(CPPFLAGS)
AC_SUBST(LDFLAGS)

NAUTILUS_REQUIRED=3.0.0
GLIB_REQUIRED=2.28.0
GTK_REQUIRED=3.0.0

PKG_CHECK_MODULES(NAUTILUS,
[
	libnautilus-extension >= $NAUTILUS_REQUIRED
	gtk+-3.0 >= $GTK_REQUIRED
	glib-2.0 >= $GLIB_REQUIRED
	gio-2.0 >= $GLIB_REQUIRED
])
AC_SUBST(NAUTILUS_CFLAGS)
AC_SUBST(NAUTILUS_LIBS)

dnl -----------------------------------------------------------
dnl Use correct nautilus extensions directory
dnl -----------------------------------------------------------
AC_ARG_WITH(nautilusdir,
	    AS_HELP_STRING([--with-nautilusdir=DIR],[Installation path for Nautilus extension @<:@auto@:>@]),
	    [ac_with_nautilusdir=$withval],
	    [ac_with_nautilusdir=""])
if test "${ac_with_nautilusdir}" = ""; then
	ac_with_nautilusdir=`pkg-config --variable=extensiondir libnautilus-extension`
fi

AC_MSG_NOTICE([installing nautilus plugin in ${ac_with_nautilusdir}])
AC_SUBST([NAUTILUS_EXTENSION_DIR],[${ac_with_nautilusdir}])

AC_CONFIG_FILES([
	Makefile
	data/Makefile
	src/Makefile
	po/Makefile.in
])

AC_OUTPUT
