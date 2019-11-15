# Process this file with autoconf to produce a configure script.

AC_INIT(libXsettings-client, 0.17, gpe@handhelds.org)
AC_CONFIG_SRCDIR([xsettings-client.c])
AM_INIT_AUTOMAKE([foreign dist-bzip2])
AM_CONFIG_HEADER(config.h)

#CFLAGS="-Os -Wall"

# Checks for programs.
AC_PROG_CC
AC_PROG_LIBTOOL

# Checks for header files.
AC_PATH_X
AC_PATH_XTRA
AC_HEADER_STDC

# Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST
AC_TYPE_PID_T

# Checks for library functions.
AC_FUNC_MALLOC
AC_FUNC_VPRINTF

# Is gtk-doc tool suite installed? We need it for documentation.
GTK_DOC_CHECK(1.0)

AC_OUTPUT(Makefile libxsettings-client.pc doc/Makefile)
