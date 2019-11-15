dnl Process this file with autoconf to produce a configure script.
AC_INIT(src/cdaudio.c)

LIBCDAUDIO_VERSION_MAJOR=0
LIBCDAUDIO_VERSION_MINOR=99
LIBCDAUDIO_VERSION_MICRO=12
LIBCDAUDIO_VERSION=$LIBCDAUDIO_VERSION_MAJOR.$LIBCDAUDIO_VERSION_MINOR.$LIBCDAUDIO_VERSION_MICRO
LIBCDAUDIO_VERSION_STRING="0.99.12p2"

PACKAGE=libcdaudio

AM_INIT_AUTOMAKE($PACKAGE, ${LIBCDAUDIO_VERSION_STRING})
AM_MAINTAINER_MODE

AM_CONFIG_HEADER(config.h)

AC_PROG_AWK
AC_PROG_CC
AC_PROG_CPP
AM_C_PROTOTYPES
AM_PROG_CC_STDC
AC_PROG_INSTALL
AC_PROG_LN_S
AC_PROG_MAKE_SET
AM_PROG_LIBTOOL

dnl AC_CANONICAL_HOST
dnl AC_ARG_PROGRAM

# We need to change the name of the installed package on some systems,
# so we don't clash with existing system files.  We'll do this by
# prefixing "lib" so it comes out as "libcdaudio.h" and
# "liblibcdaudio.so".

cdaudioname=cdaudio

threads=yes

AC_ARG_ENABLE(threads,
AS_HELP_STRING([--enable-threads],
               [build a thread-safe version of libcdaudio (default=guessed)]),
[if test "$enableval" = "yes"
then
        threads=yes
else
        threads=no
fi])

AC_ARG_ENABLE(xbox-fix,
AS_HELP_STRING([--enable-xbox-fix],
               [include fix for compilation on XBox (default=no)]),
[if test "$enableval" = "yes"
then
        xbox=1
else
        xbox=0
fi],
[xbox=0])

AC_DEFINE_UNQUOTED(XBOX, $xbox, [Nonzero if building on XBox.])

dnl POSIX.4 threads   
if test "$threads" = "yes"
then
        AC_CHECK_LIB(pthread,pthread_create,threads=-lpthread,threads=no)
        echo 'threads='$threads
        if test "$threads" = "no"
        then
                AC_CHECK_LIB(c_r,pthread_create,threads=-lc_r,threads=no)
        fi
fi

sys=generic

case "$host" in
  *beos*)
    cdaudioname=libcdaudio
    sys=beos
    AC_DEFINE(BEOS_CDAUDIO, , [This symbol will be defined if we are compiling from a BeOS system.  In that case, we will use closesocket() instead of close(), and we won't use shutdown() at all.])
    LIBS="-lcdaudio $LIBS"
    ;;
  *irix*) 
    cdaudioname=libcdaudio
    sys=irix
    AC_DEFINE(IRIX_CDAUDIO, , [This symbol will be declared if we're compiling for an Irix system, and we have access to the Irix cdaudio library to do the dirty work.])
    LIBS="-lcdaudio -lmediad -lds $LIBS"
    ;;
  *solaris*)
    sys=solaris
    AC_DEFINE(SOLARIS_GETMNTENT, , [Quick fix for Solaris.])
    AC_DEFINE(BROKEN_SOLARIS_LEADOUT, , [Another quick fix.])
    ;;
esac

AM_CONDITIONAL([IRIX], [test "$sys" = irix])
AM_CONDITIONAL([BEOS], [test "$sys" = beos])

AC_HEADER_DIRENT
AC_HEADER_STDC
AC_CHECK_HEADERS(fcntl.h sys/ioctl.h unistd.h linux/cdrom.h linux/ucdrom.h sys/cdrom.h sys/cdio.h io/cam/cdrom.h stdarg.h mntent.h sys/mntent.h sys/types.h sys/param.h sys/ucred.h sys/mount.h strings.h,,,
[[#if defined (HAVE_SYS_TYPES_H)
# include <sys/types.h>
#endif

#if defined (HAVE_SYS_PARAM_H)
# include <sys/param.h>
#endif
]])

AC_C_CONST

case "$cross_compiling" in
  yes) 
    echo "You are cross compiling.  You will need to edit config.h and specify the target machine's endianness and word size manually."
    ;;
  no)
    AC_C_BIGENDIAN
    AC_CHECK_SIZEOF(long)
    ;;
esac

AC_HEADER_TIME

AC_PROG_GCC_TRADITIONAL
AC_FUNC_VPRINTF
AC_CHECK_FUNCS(gethostbyname gethostbyname_r mkdir socket strerror strstr strtol snprintf getmntinfo strtoul)
AC_FUNC_GETMNTENT

if test "$threads" != "no"
then
        AC_DEFINE(HAVE_PTHREAD, , [Define if your system provides POSIX.4 threads.])
        CFLAGS="$CFLAGS -D_REENTRANT"
        LIBRARY_LIB="$threads $LIBRARY_LIB"
        REENTRANT="-D_REENTRANT"
fi

AC_SUBST(REENTRANT)
AC_SUBST(LIBS)
AC_SUBST(LIB_LDADD)
AC_SUBST(LIBCDAUDIO_VERSION)
AC_SUBST(LIBCDAUDIO_VERSION_MAJOR)
AC_SUBST(LIBCDAUDIO_VERSION_MINOR)
AC_SUBST(LIBCDAUDIO_VERSION_MICRO)
AC_SUBST(cdaudioname)

AC_OUTPUT([libcdaudio.pc libcdaudio-config Makefile src/Makefile
src/cdaudio.h], [chmod +x libcdaudio-config])

echo
echo Ready to build libcdaudio $LIBCDAUDIO_VERSION_STRING.
echo
case $sys in
     (irix)
        echo "* I am configured for IRIX."
        ;;
     (beos)
        echo "* I am configured for BeOS."
        ;;
     (solaris)
        echo "* I am configured Solaris."
        ;;
     (*)
        echo "* I am configured for a generic or GNU or GNU-like system."
        ;;
esac
if test "$cross_compiling" = yes
then
        echo "* The build is a cross-compilation."
else
        echo "* The build is not a cross-compilation."
fi
if test $threads != no
then
        echo "* I will build a thread-safe version."
else
        echo "* I will build a non-thread-safe version."
fi
if test $xbox = 1
then
        echo "* I will use the XBox fix."
else
        echo "* I will not use the XBox fix."
        echo "  If you're compiling on XBox, consider enabling the fix"
        echo "  with --enable-xbox-fix."
fi
echo
echo "=> If you want to help, please contact the maintainer."
echo "   libcdaudio cannot evolve as long as there is no portability testing."
echo "   We need people who can compile & test libcdaudio on:"
echo "   OpenBSD  FreeBSD  NetBSD  Solaris  Irix  BeOS  OSF/1  XBox/MythTV"
echo "   If you use a box with one of these operating systems, please consider"
echo "   helping us."
echo "   Thanks."
echo
echo 'You may build libcdaudio with your favorite Make program, e.g. "make".'
