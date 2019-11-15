#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ(2.59)
AC_INIT(flpsed, 0.7.3, Johannes.Hofmann@gmx.de)
AM_INIT_AUTOMAKE
AC_CONFIG_SRCDIR([src/GsWidget.H])
AC_CONFIG_HEADER(config.h)

CPPFLAGS="-Wall $CPPFLAGS"

# Checks for programs.
AC_PROG_CXX
AC_PROG_CC

AC_LANG_CPLUSPLUS

# Checks for libraries.

# Checks for header files.
AC_HEADER_STDC
AC_HEADER_SYS_WAIT
AC_CHECK_HEADERS([fcntl.h stdlib.h string.h unistd.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_HEADER_STDBOOL
AC_C_CONST
AC_TYPE_OFF_T
AC_TYPE_PID_T

# Checks for library functions.
AC_FUNC_FORK
AC_FUNC_MALLOC
AC_FUNC_REALLOC
AC_TYPE_SIGNAL
AC_CHECK_FUNCS([dup2 setenv strchr strdup strrchr strstr])

# Check for fltk
AC_PATH_PROG(FLTKCONFIG,fltk-config)
if test "x$FLTKCONFIG" = x; then
	echo "fltk-config not found"
	exit 1
fi
CFLAGS="`$FLTKCONFIG --cflags` $CFLAGS"
CXXFLAGS="`$FLTKCONFIG --cflags` $CXXFLAGS"
LIBS="`$FLTKCONFIG --ldflags` $LIBS"

# Check for X11
AC_CHECK_LIB([X11], [open], [], [echo "Error: libX11.so not found."; exit 1;])

AC_CONFIG_FILES([Makefile src/Makefile])
AC_OUTPUT
