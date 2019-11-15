dnl *
dnl * Process this file with autoconf to produce a configure script.
dnl *
AC_INIT(freepwing, 1.5)
AC_CONFIG_SRCDIR(src/BaseText.pm)
AC_PREREQ(2.54)
AM_INIT_AUTOMAKE

dnl *
dnl * --with-pkgdocdir option.
dnl *
AC_ARG_WITH(pkgdocdir,
AC_HELP_STRING([--with-pkgdocdir=DIR],
    [HTML documents in DIR [[default=DATADIR/freepwing/doc]]]),
[pkgdocdir="${withval}"],[pkgdocdir='${datadir}/freepwing/doc'])
AC_SUBST(pkgdocdir)

dnl *
dnl * Perl5 command.
dnl *
AC_PATH_PROGS(PERL, perl5 perl, no)
if test "$PERL" = no ; then
    AC_MSG_ERROR(perl5 not found)
fi
$PERL -e 'close(STDERR); require 5.005'
if test $? -ne 0 ; then
    AC_MSG_ERROR($PERL is older than version 5.005)
fi

AC_ARG_WITH(perllibdir,
AC_HELP_STRING([--with-perllibdir=DIR], [Perl5 modules in DIR]),
[perllibdir="${withval}"],
[perllibdir="`$PERL -e 'for(@INC){print,exit if m|/site_perl|}print $INC[[0]]'`"])
AC_MSG_CHECKING(for Perl5 module directory)
AC_MSG_RESULT($perllibdir)
AC_SUBST(perllibdir)

dnl *
dnl * sort command.
dnl *
AC_PATH_PROGS(SORT, sort, no)
if test "$SORT" = no ; then
   AC_MSG_ERROR(sort not found)
fi

dnl *
dnl * GNU make command.
dnl *
AC_PATH_PROGS(GNUMAKE, gnumake gmake make, no)
if test "$GNUMAKE" = no ; then
    AC_MSG_ERROR(GNU make not found)
fi
$GNUMAKE --help > /dev/null
if test $? -ne 0 ; then
    AC_MSG_ERROR($GNUMAKE is not GNU make)
fi

dnl * 
dnl * Output Files.
dnl * 
AC_CONFIG_FILES([Makefile src/Makefile fpwutils/Makefile doc/Makefile
    catdump/Makefile])
AC_OUTPUT
