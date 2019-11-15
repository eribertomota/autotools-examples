AC_INIT(renattach, 1.2.4)
AM_INIT_AUTOMAKE
AC_CONFIG_SRCDIR(src/renattach.c)
AC_CONFIG_HEADER(config.h)
AC_PROG_CC
AC_PROG_INSTALL
AC_HEADER_STDC
AC_CHECK_HEADERS(getopt.h memory.h stdlib.h string.h strings.h signal.h syslog.h unistd.h)
AC_C_CONST
AC_FUNC_MALLOC
AC_CHECK_FUNCS(execv fork ftruncate memset pipe strcasecmp strchr strncasecmp strrchr strstr getopt_long)
AC_CONFIG_FILES(Makefile src/Makefile conf/Makefile)
AC_OUTPUT
