dnl Process this file with autoconf to produce a configure script.
AC_INIT([cutils],[1.6],[Sandro Sigala <sandro@sigala.it>])
AC_CONFIG_HEADER([config.h])

dnl Checks for programs.
AC_PROG_CC
AC_PROG_INSTALL
AC_PROG_RANLIB
AC_PROG_LEX
AC_DECL_YYTEXT
AC_PROG_YACC

dnl Checks for libraries.
AC_REPLACE_FUNCS(err xmalloc xrealloc xstrdup)

dnl Checks for header files.
AC_HEADER_DIRENT
AC_HEADER_STDC
AC_CHECK_HEADERS(unistd.h)

dnl Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST

dnl Checks for library functions.
AC_FUNC_MEMCMP
AC_FUNC_VPRINTF
AC_CHECK_FUNCS(strerror)

AC_OUTPUT(Makefile doc/Makefile lib/Makefile \
src/Makefile src/cdecl/Makefile src/chilight/Makefile \
src/cobfusc/Makefile src/cundecl/Makefile src/cunloop/Makefile \
src/yyextract/Makefile src/yyref/Makefile)

AH_BOTTOM([#include "conf_post.h"])
