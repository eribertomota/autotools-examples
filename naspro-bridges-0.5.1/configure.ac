dnl
dnl NASPRO - The NASPRO Architecture for Sound PROcessing
dnl A collection of bridges to LV2
dnl
dnl Copyright (C) 2007-2014 Stefano D'Angelo
dnl
dnl See the COPYING file for license conditions.
dnl

AC_PREREQ([2.69])

AC_INIT([NASPRO bridges], [0.5.1], [zanga.mail@gmail.com])
AC_COPYRIGHT([Copyright (C) 2007-2014 Stefano D'Angelo])

AC_CONFIG_SRCDIR([ladspa/internal.h])
AC_CONFIG_HEADERS([config.h])
AC_CONFIG_MACRO_DIR([m4])

AM_INIT_AUTOMAKE

# Command line options.
AC_MSG_CHECKING([where to put LV2 bundles])
AC_ARG_WITH([lv2dir],
	    AS_HELP_STRING([--with-lv2dir=DIR],
	    [where to put LV2 bundles @<:@LIBDIR/lv2@:>@]),
	    [lv2dir="${withval}"], [lv2dir="${libdir}/lv2"])
AC_SUBST([lv2dir])
AC_MSG_RESULT([$lv2dir])

# Checks for programs.
AC_PROG_CC_C99
AC_DISABLE_STATIC
AC_LIBTOOL_WIN32_DLL
AC_PROG_LIBTOOL

# Checks for libraries.
PKG_CHECK_MODULES([NABRIT], [nabrit-3 >= 0.4.1])

# Checks for header files.
AC_CHECK_HEADER([ladspa.h], [build_ladspa=yes], [build_ladspa=no])
lrdfinst=no
if test $build_ladspa = yes; then
  lrdfinst=yes
  AC_MSG_CHECKING([whether LRDF-equivalent LV2 bundles should be installed])
  AC_ARG_ENABLE([lrdf-bundles],
		AS_HELP_STRING([--enable-lrdf-bundles],
		[install LRDF-equivalent LV2 bundles @<:@default=yes@:>@]),
		[lrdfinst="${enableval}"], [lrdfinst=yes])
  if test "$lrdfinst" != no; then
    lrdfinst=yes
  fi
  AC_MSG_RESULT([$lrdfinst])
fi
AM_CONDITIONAL([INSTALL_LRDF], [test $lrdfinst = yes])
AM_CONDITIONAL([BUILD_LADSPA], [test $build_ladspa = yes])

PKG_CHECK_MODULES([DSSI], [dssi >= 1.0.0], [build_dssi=yes], [build_dssi=no])
if test $build_dssi = yes; then
	PKG_CHECK_MODULES([ALSA], [alsa], [],
			  [PKG_CHECK_MODULES([ALSA], [libdssialsacompat], [],
					     [build_dssi=no])])
fi
dssi_presets=no
if test $build_dssi = yes; then
  dssi_presets=yes
  AC_MSG_CHECKING([whether to enable bridging of DSSI programs as LV2 presets])
  AC_ARG_ENABLE([dssi-presets],
		AS_HELP_STRING([--enable-dssi-presets],
		[bridge DSSI programs as LV2 presets @<:@default=yes@:>@]),
		[dssi_presets="${enableval}"], [dssi_presets=yes])
  if test "$dssi_presets" != no; then
    dssi_presets=yes
    AC_DEFINE([ENABLE_DSSI_PRESETS], [1],
	      [Define to 1 to enable bridging of DSSI programs as LV2 presets.])
  fi
  AC_MSG_RESULT([$dssi_presets])
fi
AM_CONDITIONAL([BUILD_DSSI], [test $build_dssi = yes])

# Checks for typedefs, structures, and compiler characteristics.

# Checks for library functions.

# Output.
oldmodule=$module
module=yes
eval MODULE_EXT=$shrext_cmds
module=$oldmodule
AC_SUBST([MODULE_EXT])
AC_DEFINE_UNQUOTED([MODULE_EXT], ["$MODULE_EXT"],
		   [Dynamically loadable libraries filename extension.])

AC_CONFIG_FILES([Makefile ladspa/manifest.ttl ladspa/Makefile \
		 ladspa/data/Makefile dssi/manifest.ttl dssi/Makefile])
AC_OUTPUT

AC_MSG_NOTICE([LADSPA bridge:                  $build_ladspa])
AC_MSG_NOTICE([  LRDF-equivalent bundles:      $lrdfinst])
AC_MSG_NOTICE([DSSI bridge:                    $build_dssi])
AC_MSG_NOTICE([  DSSI programs as LV2 presets: $dssi_presets])
