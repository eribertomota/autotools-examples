AC_INIT([videotrans], [1.6.1], [videotrans@berkvens.net], [videotrans])
AC_PREREQ([2.53])
AC_CONFIG_HEADERS([config.h])
AC_REVISION([$Version:$])
AC_CONFIG_SRCDIR([zoomcalc.c])
AC_CONFIG_AUX_DIR([../ac-support])

AC_PROG_INSTALL
AC_PROG_CC

if test "$CC" = gcc
then
	CFLAGS="$CFLAGS -ansi -pedantic -Wall"
fi

LIBS=""
DEFINES=""
AC_CHECK_LIB([m], [floor], [LIBS="$LIBS -lm";])
AC_SUBST([LIBS])
AC_SUBST([DEFINES])

AC_CHECK_HEADERS([unistd.h])
AC_CHECK_HEADERS([math.h])

AC_PROG_MAKE_SET
AC_CONFIG_FILES(Makefile movie-title movie-to-dvd movie-make-title movie-make-title-simple movie-rip-epg.data)
AC_OUTPUT
