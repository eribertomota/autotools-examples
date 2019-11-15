dnl Process this file with autoconf to produce a configure script.
AC_INIT(libwibble, [1.1], [libapt-front-devel@lists.alioth.debian.org])
AC_CONFIG_SRCDIR([configure.ac])
dnl AC_CONFIG_AUX_DIR(admin)
AM_INIT_AUTOMAKE([foreign subdir-objects nostdinc])

AC_ARG_ENABLE(docs,
		[  --enable-docs    Turn on generation of documentation],
		[case "${enableval}" in
			yes) docs=true ;;
			no)  docs=false ;;
			*) AC_MSG_ERROR(bad value ${enableval} for --enable-docs) ;;
		esac],[docs=true])
AM_CONDITIONAL(DO_DOCS, test x$docs = xtrue)

dnl Doen not work when embedded
dnl AC_CONFIG_HEADERS(wibble/config.h)

dnl To use subdirs
AC_PROG_MAKE_SET

AC_LANG([C++])

AC_ISC_POSIX
AC_PROG_CC
AC_PROG_CXX
AM_PROG_CC_STDC
AC_HEADER_STDC

AM_PROG_CC_C_O

dnl Support large files on 32bit systems
AC_SYS_LARGEFILE
AC_FUNC_FSEEKO

#AM_PROG_LEX
#AC_PROG_YACC

dnl Use libtool
AM_ENABLE_STATIC
AM_DISABLE_SHARED
AM_PROG_LIBTOOL

if test x"$GXX" = x"yes"; then
	CXXFLAGS="-Wall -W $CXXFLAGS"
fi

AM_CONDITIONAL([WIBBLE_STANDALONE], [true])

AC_CONFIG_FILES([
Makefile
wibble/Makefile
wibble/tests/Makefile
wibble/libwibble.pc
doc/Makefile
doc/wibble.dox
])
AC_OUTPUT

