AC_INIT([videotrans], [1.6.1], [videotrans@berkvens.net], [videotrans])
AC_PREREQ([2.53])
AC_REVISION([$Version:$])
AC_CONFIG_SRCDIR([aspects.txt])
AC_CONFIG_AUX_DIR([ac-support])

AC_PROG_INSTALL

[videotrans_warnings=""]
AC_PROG_MAKE_SET
AC_CONFIG_FILES(Makefile)
AC_CONFIG_SUBDIRS(src man1 data)
AC_OUTPUT

[if test "x$videotrans_warnings" = x ; then true ; else echo ; echo "WARNING: $videotrans_warnings" >&2 ; fi]

[true]
