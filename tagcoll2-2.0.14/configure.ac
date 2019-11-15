dnl Process this file with autoconf to produce a configure script.

AC_INIT(tagcoll2, [2.0.14], [enrico@debian.org])
AC_CONFIG_SRCDIR([configure.ac])
AM_CONFIG_HEADER(config.h)
AM_INIT_AUTOMAKE([foreign subdir-objects])

AC_ARG_ENABLE(docs,
		[  --enable-docs    Turn on generation of documentation],
		[case "${enableval}" in
			yes) docs=true ;;
			no)  docs=false ;;
			*) AC_MSG_ERROR(bad value ${enableval} for --enable-docs) ;;
		esac],[docs=true])
AM_CONDITIONAL(DO_DOCS, test x$docs = xtrue)

AC_LANG([C++])

dnl Add options for local configuration

dnl To use subdirs
AC_PROG_MAKE_SET

AC_ISC_POSIX
AC_PROG_CXX()
AC_PROG_CXXCPP
AM_PROG_CC_STDC
AC_HEADER_STDC

AM_PROG_CC_C_O
AM_PROG_LEX
AC_PROG_YACC

AM_DISABLE_SHARED

dnl Use libtool
AM_PROG_LIBTOOL

LIBWIBBLE_DEFS

LIBTAGCOLL_VERSION_INFO=`echo $VERSION | awk -F. '{ printf "%d:%d:%d", $1+$2, $3, $2 }'`
AC_SUBST(LIBTAGCOLL_VERSION_INFO)

dnl TODO: add looking for zlib

dnl Add the languages which your application supports here.
dnl ALL_LINGUAS="fr da es no it"
dnl ALL_LINGUAS="it"
dnl ALL_LINGUAS=""
dnl AM_GNU_GETTEXT

dnl Controlla se c'e' libpthread
dnl AC_CHECK_HEADERS(pthread.h)
dnl AC_CHECK_LIB(pthread, pthread_create)

dnl Look for perl
dnl AC_PATH_PROG(PERL, "perl")
dnl AC_SUBST(PERL)

CXXFLAGS="$CXXFLAGS -Wall"

AC_CHECK_FUNC([fmemopen], [have_fmemopen=yes], [have_fmemopen=no])
AM_CONDITIONAL([NO_FMEMOPEN], [test $have_fmemopen = 'no'])

AC_CONFIG_FILES([
Makefile
tagcoll/Makefile
tagcoll/tagexpr/Makefile
bench/Makefile
doc/Makefile
tools/Makefile
libtagcoll2.pc
])
AC_OUTPUT
