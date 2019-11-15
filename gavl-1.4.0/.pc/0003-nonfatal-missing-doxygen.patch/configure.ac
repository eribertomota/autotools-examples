dnl Process this file with autoconf to produce a configure script.

AC_INIT(include/gavl/gavl.h)

AM_CONFIG_HEADER(include/gavl/config.h)

AM_INIT_AUTOMAKE(gavl, 1.4.0)

GAVL_VERSION=$VERSION

GAVL_VERSION_MAJOR=`echo $VERSION | cut -d . -f 1`
GAVL_VERSION_MINOR=`echo $VERSION | cut -d . -f 2`
GAVL_VERSION_MICRO=`echo $VERSION | cut -d . -f 3 | cut -d p -f 1`

LTVERSION_CURRENT="1"
LTVERSION_REVISION="0"
LTVERSION_AGE="0"

SAVE_CFLAGS=$CFLAGS

AC_SUBST(GAVL_VERSION)
AC_SUBST(GAVL_VERSION_MAJOR)
AC_SUBST(GAVL_VERSION_MINOR)
AC_SUBST(GAVL_VERSION_MICRO)

AC_SUBST(LTVERSION_CURRENT)
AC_SUBST(LTVERSION_REVISION)
AC_SUBST(LTVERSION_AGE)

AC_CANONICAL_HOST

AC_DISABLE_STATIC

AC_PROG_LIBTOOL
AM_PROG_LIBTOOL

AC_PROG_MAKE_SET

CFLAGS=$SAVE_CFLAGS

dnl
dnl Doxygen
dnl

test_doxygen="true"
have_doxygen="false"

AC_ARG_WITH(doxygen,
    AC_HELP_STRING([--without-doxygen],
    [disable documentation generation]),
    test_doxygen="false")

if test "x$test_doxygen" = "xtrue"; then
  AC_CHECK_PROG(DOXYGEN, doxygen, "doxygen")
  if test -z "$DOXYGEN"; then
    AC_MSG_ERROR([Doxygen not found, use --without-doxygen to disable documentation generation])
  else
    have_doxygen="true"
  fi
fi

AM_CONDITIONAL(HAVE_DOXYGEN, test "x$have_doxygen" = "xtrue")

dnl
dnl Check for compiler flags
dnl  

AC_C_ATTRIBUTE_ALIGNED

AC_C_BIGENDIAN(,,AC_MSG_ERROR("Cannot detect endianess"))

dnl
dnl Check for Dependencies package
dnl

GMERLIN_DEP_DIR=/opt/gmerlin

if test -d $GMERLIN_DEP_DIR; then
  have_opt_gmerlin="true"
  export PKG_CONFIG_PATH=$GMERLIN_DEP_DIR/lib/pkgconfig:$PKG_CONFIG_PATH
  GMERLIN_DEP_CFLAGS="-I$GMERLIN_DEP_DIR/include"
  GMERLIN_DEP_LDPATH="$GMERLIN_DEP_DIR/lib"
  GMERLIN_DEP_LIBS="-L$GMERLIN_DEP_DIR/lib"
  AC_MSG_CHECKING(for --rpath option)
  OLD_LDFLAGS=$LDFLAGS
  LDFLAGS="$LDFLAGS -Wl,--rpath -Wl,$GMERLIN_DEP_DIR/lib"  
  AC_TRY_LINK([],[],
              [GMERLIN_DEP_RPATH="-Wl,--rpath -Wl,$GMERLIN_DEP_DIR/lib"; AC_MSG_RESULT(Supported)],
	      [GMERLIN_DEP_RPATH="";AC_MSG_RESULT(Unsupported)])
  LDFLAGS=$OLD_LDFLAGS
else
  have_opt_gmerlin="false"
  GMERLIN_DEP_CFLAGS=""
  GMERLIN_DEP_LDPATH=""
  GMERLIN_DEP_LIBS=""
  GMERLIN_DEP_RPATH=""
fi

LDFLAGS="$GMERLIN_DEP_RPATH"
AC_SUBST(GMERLIN_DEP_LIBS)

LIBGAVL_LIBS=""
LIBGAVL_LDFLAGS=""

dnl
dnl Check for mingw
dnl

case "$host" in
	*-*-mingw*|*cygwin*)
	os_win32=yes		
	AC_MSG_WARN([host is $host])
	;;
	*)
	os_win32=no
	;;
esac
AM_CONDITIONAL(OS_WIN32, [test "$os_win32" = "yes"])

if test "$os_win32" = "yes"; then
LIBGAVL_LIBS="-lws2_32 $LIBGAVL_LIBS"

dnl it appears that -no-undefined is necessary in mingw in order to build dll
dnl maybe we should check here if the user only wants static libs

LIBGAVL_LDFLAGS="-no-undefined $LIBGAVL_LDFLAGS"
fi

dnl
dnl Check for library functions
dnl 

AC_CHECK_FUNCS([memalign])
AC_CHECK_FUNCS([sched_setaffinity])

dnl
dnl clock_gettime
dnl

AH_TEMPLATE([HAVE_CLOCK_GETTIME],
            [clock_gettime available?])
AH_TEMPLATE([HAVE_CLOCK_MONOTONIC],
            [CLOCK_MONOTONIC available?])

HAVE_CLOCK_GETTIME="true"
HAVE_CLOCK_MONOTONIC="false"

OLD_LIBS=$LIBS
AC_SEARCH_LIBS([clock_gettime], [rt], , HAVE_CLOCK_GETTIME="false")
RT_LIBS=$LIBS
AC_SUBST(RT_LIBS)
LIBS=$OLD_LIBS

if test "x$HAVE_CLOCK_GETTIME" = "xtrue"; then
  AC_DEFINE([HAVE_CLOCK_GETTIME])

OLD_LIBS=$LIBS
LIBS=$RT_LIBS

AC_MSG_CHECKING(for CLOCK_MONOTONIC)

AC_TRY_RUN([
  #include <time.h>
  #include <errno.h>
main()
  {
  struct timespec tp;
  if(clock_gettime(CLOCK_MONOTONIC, &tp))
    return -1;
  else
    return 0;
  }
  ],
  [
    # program could be run
    AC_MSG_RESULT(yes)
    HAVE_CLOCK_MONOTONIC="true"

  ],
    # program could not be run
    AC_MSG_RESULT(no)
)

if test "x$HAVE_CLOCK_MONOTONIC" = "xtrue"; then
  AC_DEFINE([HAVE_CLOCK_MONOTONIC])
fi

fi



dnl
dnl lrint, lrintf
dnl

AC_C99_FUNC_LRINT
AC_C99_FUNC_LRINTF

AC_CHECK_HEADERS(sys/times.h byteswap.h)

dnl
dnl Check for libpng (only needed for some tests)
dnl

GMERLIN_CHECK_LIBPNG

dnl
dnl Build optimization flags
dnl

LQT_OPT_CFLAGS($host_cpu, ["-O3 -funroll-all-loops -fomit-frame-pointer -ffast-math"])

dnl
dnl Check for SIMD
dnl

GAVL_CHECK_SIMD($host_cpu, "$OPT_CFLAGS")

dnl
dnl Now, build the final CFLAGS.
dnl 

CFLAGS="$CFLAGS $OPT_CFLAGS"

LQT_TRY_CFLAGS([-Wall], CFLAGS="$CFLAGS -Wall")
LQT_TRY_CFLAGS([-Wmissing-declarations], CFLAGS="$CFLAGS -Wmissing-declarations" )
LQT_TRY_CFLAGS([-Wdeclaration-after-statement], CFLAGS="$CFLAGS -Wdeclaration-after-statement")
LQT_TRY_CFLAGS([-mfpmath=387], CFLAGS="$CFLAGS -mfpmath=387")
LQT_TRY_CFLAGS([-fvisibility=hidden], CFLAGS="$CFLAGS -fvisibility=hidden")

dnl
dnl Stuff from libsamplerate
dnl

AC_ARG_ENABLE(cpu-clip,
    AC_HELP_STRING([--disable-cpu-clip], [disable tricky cpu specific clipper]),
    ac_arg_cpu_clip="N", ac_arg_cpu_clip="Y")

if test x$ac_arg_cpu_clip = "xY" ; then
        AC_C_CLIP_MODE
else
        echo "checking processor clipping capabilities... disabled"
        ac_cv_c_clip_positive=0
        ac_cv_c_clip_negative=0
        fi

AC_DEFINE_UNQUOTED(CPU_CLIPS_POSITIVE, ${ac_cv_c_clip_positive},
        [Target processor clips on positive float to int conversion.])
AC_DEFINE_UNQUOTED(CPU_CLIPS_NEGATIVE, ${ac_cv_c_clip_negative},
        [Target processor clips on negative float to int conversion.])

AC_CHECK_SIZEOF(int,0)
AC_CHECK_SIZEOF(long,0)
AC_CHECK_SIZEOF(float,4)
AC_CHECK_SIZEOF(double,8)

dnl UD_CHECK_IEEE

dnl Absolute src path for doxygen

TOP_SRCDIR=`cd ${srcdir} && pwd` 
AC_SUBST(TOP_SRCDIR)

dnl
dnl Output variables
dnl

INCLUDES='-I$(top_srcdir)/include -I$(top_srcdir)/include/gavl -I$(top_builddir)/include'
AC_SUBST(INCLUDES)

LIBGAVL_CFLAGS=-D__GAVL__
AC_SUBST(LIBGAVL_CFLAGS)

AC_SUBST(LIBGAVL_LIBS)	
AC_SUBST(LIBGAVL_LDFLAGS)	

AC_OUTPUT(Makefile \
gavl.spec \
gavl.pc \
doc/Makefile \
doc/Doxyfile \
src/Makefile \
m4/Makefile \
utils/Makefile \
include/Makefile \
include/gavl/Makefile \
include/gavl/gavl_version.h \
gavl/Makefile \
gavl/libgdither/Makefile \
gavl/libsamplerate/Makefile \
gavl/c/Makefile \
gavl/hq/Makefile \
gavl/mmx/Makefile \
gavl/mmxext/Makefile \
gavl/3dnow/Makefile \
gavl/sse/Makefile \
gavl/sse2/Makefile \
gavl/sse3/Makefile )

