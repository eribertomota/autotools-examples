# Process this file with autoconf to produce a configure script.
AC_PREREQ(2.52)
AC_INIT(tvtime, 1.0.11, http://linuxtv.org/)
AC_CONFIG_SRCDIR([src/tvtime.c])
AM_INIT_AUTOMAKE([foreign subdir-objects])
AM_CONFIG_HEADER(config.h)
m4_ifdef([AM_SILENT_RULES], [AM_SILENT_RULES([yes])])
AM_MAINTAINER_MODE
AC_CANONICAL_HOST
AC_CONFIG_MACRO_DIR([m4])
if test x"$host_alias" = x""; then host_alias="$host"; fi

# Check for compilers.
AC_PROG_CC
AM_PROG_CC_C_O
AC_CHECK_PROG(found_cc, "$CC", yes, no)
test "x$found_cc" = "xyes" || exit 1

AC_PROG_CXX
AC_CHECK_PROG(found_cxx, "$CXX", yes, no)
test "x$found_cxx" = "xyes" || exit 1

# Check for libtool.
AC_PROG_LIBTOOL

# Checks for header files.
AC_HEADER_STDC
AC_CHECK_HEADERS([ctype.h dirent.h errno.h fcntl.h getopt.h langinfo.h math.h netinet/in.h pwd.h signal.h stdint.h stdio.h stdlib.h string.h sys/ioctl.h sys/mman.h sys/resource.h sys/stat.h sys/time.h sys/wait.h sys/types.h unistd.h wordexp.h locale.h])

AC_CHECK_HEADER([linux/videodev2.h], [], AC_MSG_ERROR(linux/videodev2.h not found))

# Checks for typedefs, structures, and compiler characteristics.
AC_HEADER_TIME

# Checks for library functions.
AC_PROG_GCC_TRADITIONAL
AC_FUNC_MMAP
AC_CHECK_FUNCS([asprintf atexit fork execlp getopt_long getpriority gettimeofday seteuid memset setreuid setpriority signal sigemptyset sigaction strerror vsscanf wordexp wordfree])

# Check for gettext
AM_GNU_GETTEXT_VERSION
AM_GNU_GETTEXT

dnl ---------------------------------------------
dnl zlib
dnl ---------------------------------------------
dnl Test for libz
AC_CHECK_LIB(z, gzsetparams,
        [ AC_CHECK_HEADER(zlib.h,
          have_zlib=yes
          ZLIB_LIBS="-lz",)], AC_MSG_ERROR(zlib needed))

AM_CONDITIONAL(HAVE_ZLIB, [test x"$have_zlib" = "xyes"])
AC_SUBST(ZLIB_LIBS)


dnl ---------------------------------------------
dnl libpng
dnl ---------------------------------------------
dnl Test for libpng
AC_CHECK_LIB(png, png_read_png,
        [ AC_CHECK_HEADER(png.h,
          have_libpng=yes
          PNG_LIBS="-lpng $ZLIB_LIBS -lm",)], AC_MSG_ERROR(libpng needed), "$ZLIB_LIBS" -lm)

AM_CONDITIONAL(HAVE_LIBPNG, [test x"$have_libpng" = "xyes"])
AC_SUBST(PNG_LIBS)


dnl ---------------------------------------------
dnl freetype
dnl ---------------------------------------------
dnl Test for freetype
PKG_CHECK_MODULES(TTF, freetype2)

dnl ---------------------------------------------
dnl libxml2
dnl ---------------------------------------------
dnl Test for libxml2
AC_PATH_PROG(LIBXML2_CONFIG,xml2-config,no)
if test "$LIBXML2_CONFIG" = "no" ; then
	AC_MSG_ERROR(libxml2 needed and xml2-config not found)
else
	XML2_LIBS="`$LIBXML2_CONFIG --libs`"
	XML2_FLAG="`$LIBXML2_CONFIG --cflags`"
	AC_DEFINE(HAVE_LIBXML2,,[LIBXML2 support])
fi
AC_SUBST(XML2_LIBS)
AC_SUBST(XML2_FLAG)

dnl ---------------------------------------------
dnl libasound2
dnl ---------------------------------------------
dnl Test for ALSA
AM_PATH_ALSA(1.0.9,
	[ AC_DEFINE(HAVE_ALSA,1,[Define this if you have Alsa (libasound) installed]) ],
	AC_MSG_RESULT(libasound needed and not found))
AM_CONDITIONAL(HAVE_ALSA, test x"$no_alsa" != "yes")


dnl ---------------------------------------------
dnl asound
dnl ---------------------------------------------
dnl Test for libasound
AC_CHECK_LIB(asound, snd_pcm_open,
        [ AC_CHECK_HEADER(alsa/asoundlib.h,
          have_asound=yes
          ASOUND_LIBS="-lasound",)], AC_MSG_ERROR(asound needed))

AM_CONDITIONAL(HAVE_ASOUND, [test x"$have_asound" = "xyes"])
AC_SUBST(ASOUND_LIBS)

dnl ---------------------------------------------
dnl check for gtk+-2.0
dnl ---------------------------------------------
dnl PKG_CHECK_MODULES(GTK, gtk+-2.0)
dnl AC_SUBST(GTK_CFLAGS)
dnl AC_SUBST(GTK_LIBS)


dnl ---------------------------------------------
dnl check for X11, Xv and XF86VidModeExtension
dnl ---------------------------------------------
AC_PATH_XTRA
AC_ARG_WITH([xinerama],
    [AS_HELP_STRING([--without-xinerama], [Disable Xinerama extension support (default: check)])])
if test x"$no_x" != x"yes"; then
    dnl check for Xshm
    AC_CHECK_LIB([Xext],[XShmCreateImage],
	[AC_DEFINE([HAVE_X11],,[X11 support])
	X11_CFLAGS="$X_CFLAGS"
	X11_LIBS="$X_PRE_LIBS $X_LIBS -lX11 $X_EXTRA_LIBS -lXext"

	dnl check for Xv
	AC_CHECK_LIB([Xv],[XvShmCreateImage],
	    [AC_DEFINE([HAVE_XV],,[Xv support])
	    X11_LIBS="$X11_LIBS -lXv"],,
	    [$X_PRE_LIBS $X_LIBS -lX11 $X_EXTRA_LIBS -lXext])

	if test "x$with_xinerama" != "xno"; then
		dnl check for Xinerama
		AC_CHECK_LIB([Xinerama],[XineramaQueryScreens],
		    [AC_DEFINE([HAVE_XINERAMA],,[Xinerama support])
		    X11_LIBS="$X11_LIBS -lXinerama"],,
		    [$X_PRE_LIBS $X_LIBS -lX11 $X_EXTRA_LIBS -lXext])
	fi

	dnl check for XSs
        AC_CHECK_LIB([Xss],[XScreenSaverSuspend],
            [AC_DEFINE([HAVE_XSSEXTENSION],,[XSs support])
            X11_LIBS="$X11_LIBS -lXss"],,
	    [$X_PRE_LIBS $X_LIBS -lX11 $X_EXTRA_LIBS -lXext])

	dnl check for Xvidmode
	AC_CHECK_LIB([Xxf86vm],[XF86VidModeGetModeLine],
	    [AC_DEFINE([HAVE_XF86VIDMODE],,[XF86VidModeExtension support])
	    X11_LIBS="$X11_LIBS -lXxf86vm"],,
	    [$X_PRE_LIBS $X_LIBS -lX11 $X_EXTRA_LIBS -lXext])],,
	[$X_PRE_LIBS $X_LIBS -lX11 $X_EXTRA_LIBS])
else
    AC_MSG_ERROR(X needed and no X libraries or development headers found)
fi
AC_SUBST(X11_CFLAGS)
AC_SUBST(X11_LIBS)

dnl This stuff looked kinda cool in the mpeg2dec source tree.

dnl GCC-specific flags
if test x"$GCC" = x"yes"; then

    dnl -Wall -Werror moved to the end to not disturb the configure script

    dnl -O3
    changequote(<<,>>)
    OPT_CFLAGS=`echo "$CFLAGS"|sed "s/-O[0-9]*//g;"`
    changequote([,])
    OPT_CFLAGS="$OPT_CFLAGS -O3"
    AC_TRY_CFLAGS([$OPT_CFLAGS],[CFLAGS=$OPT_CFLAGS])

    dnl -fomit-frame-pointer
    OPT_CFLAGS="$CFLAGS -fomit-frame-pointer"
    AC_TRY_CFLAGS([$OPT_CFLAGS],[CFLAGS=$OPT_CFLAGS])

    dnl -std=gnu99
    OPT_CFLAGS="$CFLAGS -std=gnu99"
    AC_TRY_CFLAGS([$OPT_CFLAGS],[CFLAGS=$OPT_CFLAGS])

    dnl arch-specific flags
    case "$host_alias" in
    i?86-* | k?-*)
	    AC_DEFINE([ARCH_X86],,[x86 architecture])
	    AC_DEFINE([ARCH_386],,[386 architecture])
	    ARCH_X86=yes
	    ARCH_386=yes
	    OPT_CFLAGS="$CFLAGS"
	    AC_TRY_CFLAGS([$OPT_CFLAGS],[CFLAGS=$OPT_CFLAGS]);;
    x86_64-*)
            AC_DEFINE([ARCH_X86],,[x86 architecture])
            AC_DEFINE([ARCH_X86_64],,[x86_64 architecture])
            ARCH_X86=yes
            ARCH_X86_64=yes;;
    ppc-* | powerpc-*)
	    OPT_CFLAGS="$CFLAGS -Wa,-m7400"
	    AC_TRY_CFLAGS([$OPT_CFLAGS],
	    [CFLAGS=$OPT_CFLAGS; AC_DEFINE([ARCH_PPC],,[ppc architecture])]);;
    sparc-* | sparc64-*)
	    OPT_CFLAGS="$CFLAGS -mcpu=ultrasparc -mvis -Wa,-Av9"
	    AC_TRY_CFLAGS([$OPT_CFLAGS],[CFLAGS=$OPT_CFLAGS]);;
    mips-sgi-irix6.*)	dnl do we need to be that specific ?
	    OPT_CFLAGS="$CFLAGS -mabi=64"
	    AC_TRY_CFLAGS([$OPT_CFLAGS],[CFLAGS=$OPT_CFLAGS]);;
    esac
elif test x"$CC" = x"tcc"; then
    dnl TenDRA portability checking compiler
    CFLAGS="-Xp -Yansi -f`pwd`/include/tendra.h"
    enable_mlib=no
    no_x=yes
    enable_sdl=no
else
    dnl non-gcc flags - we probably need exact configuration triplets here.
    case "$host_alias" in
    mips-sgi-irix6.*)
	OPT_CFLAGS="$CFLAGS -64"
	AC_TRY_CFLAGS([$OPT_CFLAGS],[CFLAGS=$OPT_CFLAGS]);;
    sparc-sun-solaris*)
	OPT_CFLAGS="$CFLAGS -xCC -fast -xO5"
	AC_TRY_CFLAGS([$OPT_CFLAGS],[CFLAGS=$OPT_CFLAGS]);;
    esac
fi
AM_CONDITIONAL(ARCH_X86, [test "$ARCH_X86" = "yes"])
AM_CONDITIONAL(ARCH_386, [test "$ARCH_386" = "yes"])
AM_CONDITIONAL(ARCH_X86_64, [test "$ARCH_X86_64" = "yes"])

dnl Checks for library functions.
AC_CHECK_FUNCS([memalign])

dnl Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST
AC_C_INLINE
AC_TYPE_SIZE_T
AC_C_BIGENDIAN
AC_C_ATTRIBUTE_ALIGNED

AC_CONFIG_FILES([
	Makefile
	docs/Makefile
	data/Makefile
	plugins/Makefile
	src/Makefile
	intl/Makefile
	po/Makefile.in
	m4/Makefile
	docs/man/Makefile
	docs/man/de/Makefile
	docs/man/en/Makefile
	docs/man/es/Makefile
])
AC_OUTPUT
