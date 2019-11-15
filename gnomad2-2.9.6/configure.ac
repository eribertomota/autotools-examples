dnl Process this file with autoconf to produce a configure script.
AC_PREREQ(2.52)
AC_INIT([gnomad2], [2.9.6], [triad@df.lth.se])
AC_CONFIG_SRCDIR([src/gnomad2.c])
AM_INIT_AUTOMAKE(AC_PACKAGE_NAME, AC_PACKAGE_VERSION)

dnl --------------------------------------------------------------------------
dnl
dnl Checks for basic stuff like compilers
dnl
dnl --------------------------------------------------------------------------

AC_LANG_C
AC_PROG_MAKE_SET
AC_PROG_INSTALL

dnl Checks for typedefs, structures, and compiler characteristics.
dnl AC_C_CONST

dnl --------------------------------------------------------------------------
dnl Too many people miss to add /usr/local/lib/pkgconfig to PKG_CONFIG_PATH
dnl this is not elegant, but will solve more problems than it creates.
dnl --------------------------------------------------------------------------

if test -d /usr/local/lib/pkgconfig ; then
   export PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/lib/pkgconfig
fi

dnl This is for some reason needed by the PKG_CHECK macro.
OSFLAGS=""
AC_SUBST(OSFLAGS)

dnl Basic deps
PKG_CHECK_MODULES(GN, \
		glib-2.0 \
		gthread-2.0 \
		libnjb >= 2.2.4
)

LIBNJB_VER=`$PKG_CONFIG --modversion libnjb`

dnl -------------------------------------------------------------------------
dnl check for GTK+ 3.0, if that fails, check for GTK+ 2.x
dnl --------------------------------------------------------------------------

PKG_CHECK_MODULES(GTK, gtk+-3.0 >= 3.2.0, found_gtk3_pkg=yes, found_gtk3_pkg=no)
if test x"$found_gtk3_pkg" = "xno" ; then
   	PKG_CHECK_MODULES(GTK, gtk+-2.0 >= 2.6.0, found_gtk2_pkg=yes, found_gtk2_pkg=no)
	if test x"$found_gtk2_pkg" = "xno" ; then
	   	AC_MSG_ERROR([*** Not even GTK+2.0 found! ***])
	else
		GTK_VER=`$PKG_CONFIG --modversion gtk+-2.0`
	fi
else
	GTK_VER=`$PKG_CONFIG --modversion gtk+-3.0`
fi


dnl --------------------------------------------------------------------------
dnl Check id3tag library separately:
dnl first try to locate it using pkg-config, then fall back on using
dnl header files only.
dnl --------------------------------------------------------------------------

PKG_CHECK_MODULES(TAG, id3tag >= 0.15, found_id3tag_pkg=yes, found_id3tag_pkg=no)
ID3TAG_VER=`pkg-config --modversion id3tag`
AC_CHECK_HEADER(id3tag.h, found_id3tag_header=yes, found_id3tag_header=no)

AC_ARG_WITH(id3tag-prefix,
    [  --with-id3tag-prefix=PFX   Prefix where id3tag library is installed (optional)], id3tag_prefix="$withval", id3tag_prefix="")

if test x"$id3tag_prefix" != "x"; then
   TAG_LIBS="-L$id3tag_prefix/lib -lid3tag -lz"
   TAG_CFLAGS="-I$id3tag_prefix/include"
else
   if test x"$found_id3tag_pkg" = "xno" ; then
      if test x"$found_id3tag_header" = xno ; then
         AC_MSG_ERROR([*** id3tag.h C header is needed (missing -dev package?) ***\n*** You might have erroneously installed id3lib instead of libid3tag ****\nThis distinction is very delicate, so PLEASE pay attention! ***])
      fi
      ID3TAG_VER=unknown
      TAG_CFLAGS=""
      TAG_LIBS="-lid3tag -lz"
   fi
fi
AC_SUBST(TAG_CFLAGS)
AC_SUBST(TAG_LIBS)

dnl --------------------------------------------------------------------------
dnl Check taglib library separately:
dnl first try to locate it using pkg-config, then fall back on using
dnl header files only.
dnl --------------------------------------------------------------------------

PKG_CHECK_MODULES(TAGLIB, taglib >= 1.4, found_taglib_pkg=yes, found_taglib_pkg=no)
TAGLIB_VER=`pkg-config --modversion taglib`
AC_CHECK_HEADER(taglib/tag_c.h, found_taglib_header=yes, found_taglib_header=no)

AC_ARG_WITH(taglib-prefix,
    [  --with-taglib-prefix=PFX   Prefix where taglib library is installed (optional)], taglib_prefix="$withval", taglib_prefix="")

if test x"$taglib_prefix" != "x"; then
   TAGLIB_LIBS="-L$taglib_prefix/lib -ltag_c"
   TAGLIB_CFLAGS="-I$taglib_prefix/include"
   have_taglib="yes"
   AC_DEFINE(HAVE_TAGLIB)
else
   if test x"$found_taglib_pkg" = "xno" ; then
      if test x"$found_taglib_header" = "xno" ; then
      	 AC_MSG_NOTICE([*** taglib was not found on your system. Deactivating Ogg/FLAC support! ***])
	 TAGLIB_VER="NOT USED"
      else
         TAGLIB_VER=unknown
      	 TAGLIB_CFLAGS=""
      	 TAGLIB_LIBS="-ltag_c"
      	 have_taglib="yes"
      	 AC_DEFINE(HAVE_TAGLIB)
      fi
   else
      have_taglib="yes"
      dnl Override the package default which is only for C++
      TAGLIB_LIBS="-ltag_c"
      AC_DEFINE(HAVE_TAGLIB)
   fi
fi
AC_SUBST(TAGLIB_CFLAGS)
AC_SUBST(TAGLIB_LIBS)
AM_CONDITIONAL(TAGLIB_COMPILE, test x"$have_taglib" = "xyes" )

AC_ARG_WITH(taglib-only, [  --with-taglib-only   Use ONLY taglib to tag even MP3 files.], taglib_only="yes", taglib_only="no")
if test x"$taglib_only" = "xyes" ; then
   AC_DEFINE(TAGLIB_ONLY)
   AC_MSG_NOTICE([*** use taglib and taglib only! ***])
fi

dnl --------------------------------------------------------------------------
dnl
dnl Check for the new, cool libmtp library, and activate functionality
dnl if we have it.
dnl
dnl --------------------------------------------------------------------------

PKG_CHECK_MODULES(MTP, libmtp >= 0.3.0, found_libmtp_pkg=yes, found_libmtp_pkg=no)
MTP_VER=`pkg-config --modversion libmtp`
AC_CHECK_HEADER(libmtp.h, found_libmtp_header=yes, found_libmtp_header=no)

AC_ARG_WITH(libmtp-prefix,
    [  --with-libmtp-prefix=PFX   Prefix where libmtp library is installed (optional)], libmtp_prefix="$withval", libmtp_prefix="")

if test x"$libmtp_prefix" != "x"; then
   MTP_LIBS="-L$libmtp_prefix/lib -lmtp"
   MTP_CFLAGS="-I$libmtp_prefix/include"
   MTP_VER=unknown
   AC_DEFINE(HAVE_LIBMTP)
else
   if test x"$found_libmtp_pkg" = "xno" ; then
      if test x"$found_libmtp_header" = xno ; then
         AC_MSG_NOTICE([*** libmtp was not found on your system. Deactivating MTP support! ***])
	 MTP_VER="NOT USED"
      else
         LIBMTP_VER=unknown
         MTP_CFLAGS=""
         MTP_LIBS="-lmtp"
         AC_DEFINE(HAVE_LIBMTP)
      fi
   else
      AC_DEFINE(HAVE_LIBMTP)
      dnl Check for libmtp 0.3.0+
      PKG_CHECK_EXISTS(libmtp >= 0.3.0, found_libmtp_030_pkg=yes, found_libmtp_030_pkg=no)
      if test x"$found_libmtp_030_pkg" = "xyes" ; then
      	 AC_DEFINE([HAVE_LIBMTP_030], 1, [indicates whether libmtp 0.3.0 is installed])
      fi
   fi
fi
AC_SUBST(MTP_CFLAGS)
AC_SUBST(MTP_LIBS)

dnl --------------------------------------------------------------------------
dnl Check gudev library separately
dnl --------------------------------------------------------------------------

PKG_CHECK_MODULES(GUDEV, gudev-1.0 >= 143, found_gudev_pkg=yes, found_gudev_pkg=no)
if test x"$found_gudev_pkg" = "xno" ; then
   GUDEV_VER="NOT USED"
else
   GUDEV_VER=`pkg-config --modversion gudev-1.0`
   AC_DEFINE(HAVE_GUDEV)
fi
AC_SUBST(GUDEV_CFLAGS)
AC_SUBST(GUDEV_LIBS)

dnl --------------------------------------------------------------------------
dnl
dnl Add some deprecation C flags
dnl
dnl --------------------------------------------------------------------------

CFLAGS="$CFLAGS -DGTK_DISABLE_SINGLE_INCLUDES"
CFLAGS="$CFLAGS -DG_DISABLE_SINGLE_INCLUDES"
dnl CFLAGS="$CFLAGS -DGTK_DISABLE_DEPRECATED"
dnl CFLAGS="$CFLAGS -DG_DISABLE_DEPRECATED"
dnl CFLAGS="$CFLAGS -DGDK_DISABLE_DEPRECATED"
dnl CFLAGS="$CFLAGS -DGTK_MULTIHEAD_SAFE"

dnl This is for the thing to build on Windows.
dnl CFLAGS="$CFLAGS -mms-bitfields"

dnl --------------------------------------------------------------------------
dnl Internationali[sz]ation
dnl --------------------------------------------------------------------------

IT_PROG_INTLTOOL([0.35.0])

GETTEXT_PACKAGE=gnomad2
AC_SUBST(GETTEXT_PACKAGE)
AC_DEFINE_UNQUOTED(GETTEXT_PACKAGE, "$GETTEXT_PACKAGE", [GetText Package])

AM_GLIB_GNU_GETTEXT

if test "x${prefix}" = "xNONE"; then
	AC_DEFINE_UNQUOTED(GNOMADLOCALEDIR, "${ac_default_prefix}/${DATADIRNAME}/locale", [Locale dir])
else
	AC_DEFINE_UNQUOTED(GNOMADLOCALEDIR, "${prefix}/${DATADIRNAME}/locale", [Locale dir])
fi

dnl --------------------------------------------------------------------------
dnl
dnl Checks for generic header files.
dnl
dnl --------------------------------------------------------------------------

AC_HEADER_DIRENT
AC_HEADER_STDC
AC_CHECK_HEADERS(malloc.h stdlib.h string.h fcntl.h inttypes.h)
AC_CHECK_FUNCS(chdir)

dnl --------------------------------------------------------------------------
dnl
dnl At last write the configured makefiles
dnl
dnl --------------------------------------------------------------------------

AC_SUBST(ac_aux_dir)
AC_OUTPUT([
Makefile
src/Makefile
doc/Makefile
po/Makefile.in
])

echo "
$PACKAGE $VERSION
Configuration :
---------------

 Source code location .: $srcdir
 C Preprocessor .......: $CPP $CPPFLAGS
 C Compiler ...........: $CC $CFLAGS
 C Linker .............: $CC $LDFLAGS $LIBS
 GTK+ version .........: $GTK_VER
 libnjb version........: $LIBNJB_VER
 libmtp version........: $MTP_VER
 id3tag version........: $ID3TAG_VER
 taglib version........: $TAGLIB_VER
 gudev version.........: $GUDEV_VER
 Install path .........: $prefix

 Now type 'make' to build $PACKAGE $VERSION,
 and then 'make install' for installation.
"
