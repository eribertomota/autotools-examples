AC_INIT(hashalot.c)
AM_INIT_AUTOMAKE(hashalot, 0.1.0)

AC_PROG_INSTALL
AC_PROG_CC
AC_PROG_LN_S

AC_HEADER_STDC
AC_CHECK_HEADERS(libgen.h stdio.h stdlib.h string.h unistd.h assert.h sys/types.h sys/mman.h endian.h , , [ AC_MSG_ERROR(required header not found)])
AC_CHECK_FUNCS(getopt snprintf , , [ AC_MSG_ERROR(required function not found)])

AC_OUTPUT(Makefile)
