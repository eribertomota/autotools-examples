dnl Process this file with autoconf to produce a configure script.

AC_INIT([upse], [1.0.0], [nenolod+upse@sacredspiral.co.uk])
AC_PREREQ([2.59])

AC_CANONICAL_HOST
AC_CANONICAL_TARGET

AC_CONFIG_HEADERS([config.h])

dnl libbeep
LIBBEEP_MAJOR_VERSION=2
LIBBEEP_MINOR_VERSION=0
LIBBEEP_MICRO_VERSION=0
LIBBEEP_VERSION=$LIBBEEP_MAJOR_VERSION.$LIBBEEP_MINOR_VERSION.$LIBBEEP_MICRO_VERSION
AC_SUBST(LIBBEEP_MAJOR_VERSION)
AC_SUBST(LIBBEEP_MINOR_VERSION)
AC_SUBST(LIBBEEP_MICRO_VERSION)

dnl XXX kludge for FreeBSD
if test -d "/usr/X11R6/include"; then
	CPPFLAGS="$CPPFLAGS -I/usr/X11R6/include"
fi

dnl append audacious header path to CPPFLAGS when --prefix is specified.
if test "$prefix" != "NONE" ; then
   CPPFLAGS="$CPPFLAGS -I${includedir}"
fi

dnl OMK bootstrap
AC_SUBST([PACKAGE], [AC_PACKAGE_TARNAME])
AC_SUBST([VERSION], [AC_PACKAGE_VERSION])

AC_DEFINE_UNQUOTED(PACKAGE, "$PACKAGE", [Name of package])
AC_DEFINE_UNQUOTED(VERSION, "$VERSION", [Version number of package])

dnl Check for C compiler

AC_PROG_CC
AC_PROG_CXX
AC_ISC_POSIX
AC_C_BIGENDIAN

if test x"$GCC" = x"yes"; then
	CFLAGS="$CFLAGS -pipe -Wall"
	CXXFLAGS="$CXXFLAGS -pipe -Wall"
fi

dnl Locate a program and check that its version is acceptable.
dnl AC_PROG_CHECK_VER(var, namelist, version-switch,
dnl 		      [version-extract-regexp], version-glob [, do-if-fail])
AC_DEFUN([AC_CHECK_PROG_VER],
[AC_CHECK_PROGS([$1], [$2])
if test -z "[$]$1"; then
  ac_verc_fail=yes
else
  # Found it, now check the version.
  AC_MSG_CHECKING([version of [$]$1])
changequote(<<,>>)dnl
  ac_prog_version=`<<$>>$1 $3 2>&1 ifelse(<<$4>>,,,
                   <<| sed -n 's/^.*patsubst(<<$4>>,/,\/).*$/\1/p'>>)`
  case $ac_prog_version in
    '') ac_prog_version="v. ?.??, bad"; ac_verc_fail=yes;;
    <<$5>>)
changequote([,])dnl
       ac_prog_version="$ac_prog_version, ok"; ac_verc_fail=no;;
    *) ac_prog_version="$ac_prog_version, bad"; ac_verc_fail=yes;;

  esac
  AC_MSG_RESULT([$ac_prog_version])
fi
ifelse([$6],,,
[if test $ac_verc_fail = yes; then
  $6
fi])
])

GCC42_CFLAGS="-fgnu89-inline"
AC_CHECK_PROG_VER(CC, ${ac_tool_prefix}gcc ${ac_tool_prefix}cc, -v,
  [version \([egcygnustpi-]*[0-9.]*\)], [4.[2-9]* ],
  GCC42_CFLAGS="")

dnl Check for assembler

AM_PROG_AS

dnl Checks for various programs

AC_PROG_LN_S
AC_PROG_MAKE_SET

AC_PATH_PROG(RM, rm)
AC_PATH_PROG(MV, mv)
AC_PATH_PROG(CP, cp)
AC_PATH_PROG(AR, ar)
AC_PATH_PROG(RANLIB, ranlib)

dnl Gettext -nenolod
AM_GNU_GETTEXT([external])

dnl Path settings

dnl Check for Audacious

UPSE_TARGET_AUD=""
AC_ARG_ENABLE(audplugin,
        [  --enable-audplugin                 enable audacious plugin (default=yes)],
                        audplugin=$enableval, audplugin=yes)

if test "x$audplugin" == "xyes"; then
	PKG_CHECK_MODULES(AUDACIOUS, [audacious >= 1.3.99],
	    [UPSE_TARGET_AUD="upse-audacious"
	         audplugin="yes"],
	    [audplugin="no"]
	)
fi

AC_SUBST(UPSE_TARGET_AUD)

AC_ARG_ENABLE(ao,
        [  --enable-ao                        enable libao support (default=yes)],
                        ao=$enableval, ao=yes)
if test "x$ao" == "xyes"; then
	PKG_CHECK_MODULES(AO, [ao],
	    [AC_DEFINE(HAVE_AO, 1, [Define this if you have AO.])],
            [ao="no"]
	)
fi

BUILDSYS_SHARED_LIB
BUILDSYS_PROG_IMPLIB

CFLAGS="$CFLAGS $EXTRA_CFLAGS"

AC_CONFIG_FILES([
	buildsys.mk
	extra.mk
])

AC_OUTPUT

echo
echo "Features:"
echo
echo "   upse123: yes"
echo "     + libao support: $ao"
echo "   audacious 1.4 plugin: $audplugin"
echo
echo "Type make to compile, and make install to install."
echo
