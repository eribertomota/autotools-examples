AC_INIT([din], [5.2.1])
AM_INIT_AUTOMAKE([foreign])
AC_CONFIG_SRCDIR([configure.ac])
AC_PROG_CXX
AC_CHECK_HEADERS([GL/gl.h],AC_MSG_NOTICE([+++ Found OpenGL +++]),[AC_MSG_ERROR([!!! Please install OpenGL !!!])])
AC_CHECK_HEADERS([tcl.h] [tcl8.5/tcl.h],AC_MSG_NOTICE([+++ Found Tcl 8.5 +++]),[AC_MSG_WARN([!!! Is Tcl 8.5 installed? !!!])])
AC_CHECK_HEADERS([libircclient.h],,[AC_MSG_ERROR([!!! Please install libircclient !!!])])
PKG_CHECK_MODULES([liblo], [liblo])
PKG_CHECK_MODULES([jack], [jack])
PKG_CHECK_MODULES([fftw3f], [fftw3f])
AC_CONFIG_FILES([Makefile src/Makefile include/Makefile data/Makefile])
AC_OUTPUT
