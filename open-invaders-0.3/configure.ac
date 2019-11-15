dnl Process this file with autoconf to produce a configure script.
dnl Created by Anjuta application wizard.

AC_INIT(open-invaders, 0.3, http://www.jamyskis.net/invaders.php)

PACKAGE_DATA_DIR=open_invadersdatadir
AC_SUBST(PACKAGE_DATA_DIR)

AC_SUBST(PACKAGE_DATA_DIR)


AC_SUBST(PACKAGE)


AC_SUBST(open_invadersincdir)


AC_SUBST(open_invadersdatadir)

AM_INIT_AUTOMAKE(AC_PACKAGE_NAME, AC_PACKAGE_VERSION)
AM_CONFIG_HEADER(config.h)
AM_MAINTAINER_MODE

AC_ISC_POSIX
AC_PROG_CXX
AM_PROG_CC_STDC
AC_HEADER_STDC






AM_PROG_LIBTOOL






PKG_CHECK_MODULES(ALLEGRO, alsa)
AC_SUBST(ALLEGRO_CFLAGS)
AC_SUBST(ALLEGRO_LIBS)

AC_OUTPUT([
Makefile
data/Makefile
headers/Makefile
src/Makefile

])
