AC_INIT([cowdancer], m4_esyscmd_s([dpkg-parsechangelog -S version]))
AC_PREREQ([2.68])
AC_CONFIG_AUX_DIR([build-aux])
AC_CONFIG_MACRO_DIR([m4])
AM_INIT_AUTOMAKE([subdir-objects])

LT_INIT
AM_MAINTAINER_MODE

dnl Check this is the right directory
AC_CONFIG_SRCDIR([cowdancer.c])

AC_PROG_CC
dnl Only needed for a single test
AC_PROG_CXX

AC_CHECK_LIB([ncurses],
             [setupterm],
             [[LIBS="-lncurses${LIBS:+ $LIBS}"] AC_CHECK_HEADER([curses.h], [], AC_MSG_FAILURE([curses.h could not be found]))],
             [AC_MSG_FAILURE([ncurses library could not be found])])

dnl The dlerror() function is in the C library for *BSD and in
dnl libdl on GLIBC-based systems
AC_SEARCH_LIBS([dlerror],
               [dl dld],
               [],
               [AC_MSG_ERROR([unable to find the dlerror() function])])

AC_CANONICAL_HOST
AC_MSG_CHECKING([whether qemubuilder is supported])
case "$host_os" in
    *linux*)
        AC_MSG_RESULT([yes])
        AM_CONDITIONAL([QEMUBUILDER], [true])
        ;;
    *)
        AC_MSG_RESULT([no])
        AM_CONDITIONAL([QEMUBUILDER], [false])
        ;;
esac

AC_SUBST([objdir], [$objdir])
AC_CONFIG_FILES([Makefile])
AC_OUTPUT
