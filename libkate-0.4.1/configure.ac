AC_INIT([libkate],[0.4.1])

AC_CONFIG_SRCDIR([include/kate/kate.h.in])
AC_CONFIG_AUX_DIR([misc/autotools])

AC_PREREQ(2.53)

AC_CANONICAL_TARGET

AM_INIT_AUTOMAKE([-Wall foreign subdir-objects])
AC_CONFIG_HEADERS([include/config.h])

ifdef([AM_SILENT_RULES],[AM_SILENT_RULES])

dnl  3. If the library source code has changed at all since the last
dnl     update, then increment REVISION (`C:R:A' becomes `C:r+1:A').
dnl
dnl  4. If any interfaces have been added, removed, or changed since the
dnl     last update, increment CURRENT, and set REVISION to 0.
dnl
dnl  5. If any interfaces have been added since the last public release,
dnl     then increment AGE.
dnl
dnl  6. If any interfaces have been removed since the last public release,
dnl     then set AGE to 0.

LIBKATE_SHARED_VERSION="4:0:3"
LIBOGGKATE_SHARED_VERSION="3:2:2"

AC_PROG_CC_C_O
AC_LIBTOOL_DLOPEN
AC_PROG_LIBTOOL
AC_PROG_LEX
AC_PROG_YACC
AC_PROG_GREP
AC_PROG_NM
AC_PROG_SED

AC_C_CONST
AC_C_INLINE


# headers

AC_HEADER_STDC
AC_CHECK_HEADERS([unistd.h time.h limits.h ctype.h])

dnl Work out which int types to use
AC_CHECK_HEADERS(
  [stdint.h],
  [
    INCLUDE_INT_HEADER="#include <stdint.h>"
    INT32_T="int32_t"
    UINT32_T="uint32_t"
    INT64_T="int64_t"
    UINT64_T="uint64_t"
  ],
  [
    AC_TYPE_INT32_T
    test "x$ac_cv_c_int32_t" = "xyes" && INT32_T="int32_t" || INT32_T=$ac_cv_c_int32_t
    AC_TYPE_UINT32_T
    test "x$ac_cv_c_uint32_t" = "xyes" && UINT32_T="uint32_t" || INT32_T=$ac_cv_c_uint32_t
    AC_TYPE_INT64_T
    test "x$ac_cv_c_int64_t" = "xyes" && INT64_T="int64_t" || INT64_T=$ac_cv_c_int64_t
    AC_TYPE_UINT64_T
    test "x$ac_cv_c_uint64_t" = "xyes" && UINT64_T="uint64_t" || INT64_T=$ac_cv_c_uint64_t
  ]
)

AC_TYPE_SIZE_T

AC_CHECK_PROG(HAVE_PKG_CONFIG,pkg-config,yes)

AC_ARG_ENABLE(doc, [  --disable-doc           Disable building documentation (default enabled)])
if test "x$enable_doc" != "xno"
then
  AC_CHECK_PROG(HAVE_DOXYGEN,doxygen,yes)
else
  HAVE_DOXYGEN="no"
fi
AM_CONDITIONAL(HAVE_DOXYGEN,test "${HAVE_DOXYGEN}" = "yes")

AC_ARG_ENABLE(valgrind, [  --enable-valgrind       Run the tests with Valgrind (default disabled)])
if test "x$enable_valgrind" = "xyes"
then
  AC_PATH_PROG(VALGRIND,valgrind,)
  if test "x$VALGRIND" != "x"
  then
    VALGRIND="$VALGRIND -q --leak-check=full --show-reachable=yes"
  fi
fi

AC_PATH_PROG(OGGZ,oggz,)
if test "x$OGGZ" != "x"
then
  OGG_MERGE="oggz merge"
  OGG_DIFF="oggz diff"
else
  AC_PATH_PROG(OGG_MERGE,oggz-merge,)
  if test "x$OGG_MERGE" = "x"
  then
    AC_PATH_PROG(OGG_MERGE,oggzmerge,)
    if test "x$OGG_MERGE" = "x"
    then
      AC_PATH_PROG(OGG_MERGE,oggmerge,)
    fi
  fi
  AC_PATH_PROG(OGG_DIFF,oggz-diff,)
  if test "x$OGG_DIFF" = "x"
  then
    AC_PATH_PROG(OGG_DIFF,oggzdiff,)
    if test "x$OGG_DIFF" = "x"
    then
      AC_PATH_PROG(OGG_DIFF,cmp,)
    fi
  fi
fi
AM_CONDITIONAL(HAVE_OGG_MERGE,test "x${OGG_MERGE}" != "x")

AM_PATH_PYTHON(, HAVE_PYTHON=yes, HAVE_PYTHON=no)
AM_CONDITIONAL(HAVE_PYTHON,test "${HAVE_PYTHON}" = "yes")

AC_CHECK_PROGS(GENHASH,md5sum md5 sha1sum)

VERSION_MAJOR=`echo $VERSION | $SED 's/\([[0-9]]*\)\.\([[0-9]]*\)\.\([[0-9]]*\)/\1/'`
VERSION_MINOR=`echo $VERSION | $SED 's/\([[0-9]]*\)\.\([[0-9]]*\)\.\([[0-9]]*\)/\2/'`
VERSION_PATCH=`echo $VERSION | $SED 's/\([[0-9]]*\)\.\([[0-9]]*\)\.\([[0-9]]*\)/\3/'`

if test "x$HAVE_PKG_CONFIG" = "xyes"
then
  PKG_CHECK_MODULES(OGG, ogg >= 1.0, HAVE_OGG=yes, HAVE_OGG=no)
fi
if test "x$HAVE_OGG" = "xno"
then
  AC_CHECK_LIB(
    ogg,
    ogg_sync_init,
    [
      AC_CHECK_HEADER(
        [ogg/ogg.h],
        [HAVE_OGG=yes],
        [HAVE_OGG=no],
      )
    ],
    [HAVE_OGG=no]
  )
fi
AM_CONDITIONAL(HAVE_OGG,test "x${HAVE_OGG}" = "xyes")

if test "x$HAVE_PKG_CONFIG" = "xyes"
then
  PKG_CHECK_MODULES(PNG, libpng, HAVE_PNG=yes, HAVE_PNG=no)
fi
if test "x$HAVE_PNG" = "xno"
then
  AC_CHECK_LIB(
    png,
    png_read_init,
    [
      AC_CHECK_HEADER(
        [png.h],
        [HAVE_PNG=yes],
        [HAVE_PNG=no],
      )
    ],
    [HAVE_PNG=no]
  )
fi
if test "x$HAVE_PNG" = "xyes"
then
  AC_DEFINE(HAVE_PNG, [1], [Define to 1 if libpng is available.])
fi
AM_CONDITIONAL(HAVE_PNG,test "${HAVE_PNG}" = "yes")

CWARNFLAGS_LIGHT=""
if test "x$GCC" = "xyes"
then
  CWARNFLAGS_LIGHT="$CWARNFLAGS_LIGHT -Wall -W"
fi

CWARNFLAGS_FULL="$CWARNFLAGS_LIGHT"

AC_ARG_ENABLE(more_warnings, [  --enable-more-warnings  Enable more warnings (default disabled)])
if test "x$enable_more_warnings" = "xyes"
then
  if test "x$GCC" = "xyes"
  then
    CWARNFLAGS_LIGHT="$CWARNFLAGS_LIGHT -Wdeclaration-after-statement -Wcast-qual -Wcast-align"
    CWARNFLAGS_LIGHT="$CWARNFLAGS_LIGHT -Winit-self -Wcast-align -pedantic -Wformat=2 -Wunused"
    CWARNFLAGS_LIGHT="$CWARNFLAGS_LIGHT -Wstrict-aliasing=2 -Wpointer-arith -Wbad-function-cast -Waggregate-return"

    CWARNFLAGS_FULL="$CWARNFLAGS_LIGHT"
    CWARNFLAGS_FULL="$CWARNFLAGS_FULL -Wshadow -Wsign-compare -Wredundant-decls -Wmissing-prototypes -Wundef -Wmissing-declarations"
  fi
fi

#ifeq ($(SPAMMY_WARNINGS),1)
#CWARNFLAGS_FULL="$CWARNFLAGS_FULL -Wconversion"
#CWARNFLAGS_LIGHT="$CWARNFLAGS_FULL"
#endif

AC_ARG_ENABLE(debug, [  --enable-debug          Enable debug code and logs (default disabled)])
if test "x$enable_debug" = "xyes"
then
  CFLAGS_DEBUG="-DDEBUG"
fi

AC_ARG_ENABLE(fortify_source, [  --enable-fortify-source Build with -D_FORTIFY_SOURCE=2 (default disabled)])
if test "x$enable_fortify_source" = "xyes"
then
  CFLAGS_FORTIFY_SOURCE="-D_FORTIFY_SOURCE=2"
fi

STREAMS="bspline kate empty demo minimal karaoke unicode path bom markup font utf8test z metadata"
STREAMS="$STREAMS style periodic granule justify"
if test "x$HAVE_PNG" = "xyes"
then
  STREAMS="$STREAMS png"
fi


AC_SUBST([LIBKATE_SHARED_VERSION])
AC_SUBST([LIBOGGKATE_SHARED_VERSION])
AC_SUBST([INCLUDE_INT_HEADER])
AC_SUBST([VERSION_MAJOR])
AC_SUBST([VERSION_MINOR])
AC_SUBST([VERSION_PATCH])
AC_SUBST([INT32_T])
AC_SUBST([UINT32_T])
AC_SUBST([INT64_T])
AC_SUBST([UINT64_T])
AC_SUBST([CONST])
AC_SUBST([CWARNFLAGS_LIGHT])
AC_SUBST([CWARNFLAGS_FULL])
AC_SUBST([CFLAGS_DEBUG])
AC_SUBST([CFLAGS_FORTIFY_SOURCE])
AC_SUBST([NM])
AC_SUBST([STREAMS])

AC_CONFIG_FILES(
  [Makefile]
  [tools/Makefile]
  [tools/KateDJ/Makefile]
  [tools/KateDJ/kdj/constants.py]
  [doc/Makefile]
  [doc/man/kateenc.1 doc/man/katedec.1 doc/man/katalyzer.1 doc/man/KateDJ.1]
  [include/kate/kate.h]
  [tests/Makefile]
  [misc/pkgconfig/kate.pc]
  [misc/pkgconfig/kate-uninstalled.pc]
  [misc/pkgconfig/oggkate.pc]
  [misc/pkgconfig/oggkate-uninstalled.pc]
  [doc/kate.doxygen]
)
AC_OUTPUT

