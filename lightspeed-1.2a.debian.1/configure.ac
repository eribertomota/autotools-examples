# configure.ac
#
# Process this file with autoconf to produce a configure script.
#

AC_PREREQ([2.67])
AC_INIT([lightspeed], [1.2b.debian.1], [Daniel Richard G. <skunk@alum.mit.edu>])
AC_CONFIG_AUX_DIR([config])
AC_CONFIG_MACRO_DIR([m4])
AC_USE_SYSTEM_EXTENSIONS

AM_CONFIG_HEADER([config.h])
AM_INIT_AUTOMAKE

# Check for programs
#
AM_SANITY_CHECK
AC_PROG_INSTALL
AC_PROG_CC
AC_PROG_CPP
AC_PROG_CXX

# Check for header files
#
AC_HEADER_STDC
AC_CHECK_HEADERS([getopt.h malloc.h sys/time.h])

# Check for typedefs, structures, and compiler characteristics.
#
AC_C_CONST
AC_TYPE_SIZE_T
AC_HEADER_TIME

# Check for library functions
#
AC_CHECK_FUNCS([getopt_long gettimeofday strcspn strdup strtod])

# Checks for GTK+ libraries.
#

AC_ARG_WITH(gtk,           [  --with-gtk=1,2       use GTK 1 or 2 (auto)])

if test "x$with_gtk" != "x1" -a "$gtkmorph_gtk" = ""  ; then
  pkg_modules="gtk+-2.0 >= 2.0.0"
  PKG_CHECK_MODULES(GTK, [$pkg_modules],
  version_of_gtk=gtk2,
  [if test  "x$with_gtk" = "x2" ; then
   AC_MSG_ERROR([ libgtk 2 is not available ])
   exit 1
  fi;])
 else
  AC_MSG_NOTICE([ Testing for GTK 2 skipped])
fi
if test "x$with_gtk" != "x2"  -a "$version_of_gtk" = "" ; then
  AC_MSG_ERROR([Cannot find proper GTK+ version])
dnl
dnl Note: We are not using GTK1 anymore
dnl
dnl  AM_PATH_GTK(1.0.1, , [AC_MSG_ERROR([Cannot find proper GTK+ version])])
dnl  version_of_gtk=gtk1
dnl  AC_DEFINE(HAVE_GTK1,1,"Define if compiled with GTK 1 and GtkGLArea ")
dnl
fi

AM_CONDITIONAL(COND_GTK1, test "$version_of_gtk" = "gtk1" )

#
# Check for OpenGL libraries
#

AC_ARG_WITH(GL-prefix, [  --with-GL-prefix=PFX    Prefix where OpenGL is installed (optional)])

GL_CFLAGS=""
GL_LDOPTS=""
if test -n "$with_GL_prefix" ; then
	GL_CFLAGS="-I$with_GL_prefix/include"
	GL_LDOPTS="-L$with_GL_prefix/lib"
fi

AC_CHECK_LIB(GL, glBegin, , AC_MSG_ERROR([OpenGL library not found.]), $GL_LDOPTS)

GL_LIBS="$GL_LDOPTS -lGL"

#
# Check for GtkGLArea widget
# or for gtkglext-1.0
#

AC_ARG_WITH(ftgl,           [  --with-ftgl  support for TrueType fonts])



if test "x$with_ftgl" = x  -o "x$with_ftgl" = xyes ; then  
   if test "$CXX" ; then
    PKG_CHECK_MODULES(
     FTGL,
     ["ftgl"], 
     [AC_DEFINE([HAVE_LIBFTGL], [1], ["Define if FTGL support for TrueType font is available"])
       with_ftgl=yes ] ,
     [AC_MSG_WARN([ftgl is not available : support for TrueType fonts is unavailable])
       with_ftgl=no
     ])
   else
     AC_MSG_WARN([ ftgl  needs a C++ compiler ])
     with_ftgl=no
   fi
   if test  "x$with_ftgl" = xyes  ; then
dnl Mennucc: TrueType fallback font
    font=${datadir}/fonts/truetype/freefont/FreeSans.ttf

    PKG_CHECK_MODULES(FC,  fontconfig >= 2.2.3,
    [ AC_DEFINE(HAVE_FC,1,"Define if fontconfig library is available")  ] ,
    [if test ! -r $font ; then
      AC_MSG_WARN( TrueType font $font is not available , please install it from http://savannah.nongnu.org/download/freefont/)
     fi] )
   fi
else
   with_ftgl=no
fi
AM_CONDITIONAL(COND_FTGL, test "x$with_ftgl" != xno )


if test "$version_of_gtk" = "gtk2" ; then
  pkg_modules="gtkglext-1.0 >= 0.7.0"
  PKG_CHECK_MODULES(GTKGL, [$pkg_modules],[ : ] ,[
    AC_MSG_ERROR([ gtkglext  is not available  ])
    exit 1 ] )

else
 AC_ARG_WITH(gtkgl-prefix, [  --with-gtkgl-prefix=PFX Prefix where GtkGLArea is installed (optional)])

 GTKGL_CFLAGS=""
 GTKGL_LDOPTS="" 
 if test -n "$with_gtkgl_prefix" ; then
	GTKGL_CFLAGS="-I$with_gtkgl_prefix/include"
	GTKGL_LDOPTS="-L$with_gtkgl_prefix/lib"
 fi


 AC_CHECK_LIB(gtkgl, gtk_gl_area_new, ,
	AC_MSG_ERROR([Cannot find GtkGLArea library.]),
	$GTKGL_LDOPTS $GTK_LIBS $GL_LIBS)

 GTKGL_LIBS="$GTKGL_LDOPTS -lgtkgl"
fi



#
# Test for libpng
#

  if test -z "$LIBPNG_LIB"; then
    AC_CHECK_LIB(png, png_read_info,
    [AC_CHECK_HEADER(png.h,
	png_ok=yes,
	png_ok=no)
    ],[
      AC_MSG_WARN([*** PNG exporter cannot be built (PNG library not found) ***])
    ],[
      -lz -lm
    ])
    if test "$png_ok" = yes; then
      AC_MSG_CHECKING([for png_structp in png.h])
      AC_TRY_COMPILE([#include <png.h>],
        [png_structp pp; png_infop info; png_colorp cmap; png_create_read_struct;],
        png_ok=yes,
        png_ok=no)
      AC_MSG_RESULT($png_ok)
      if test "$png_ok" = yes; then
        PNG='png'; LIBPNG_LIB='-lpng -lz'
      else
        AC_MSG_WARN(*** PNG exporter cannot be built (PNG library is too old) ***)
      fi
    else
      AC_MSG_WARN(*** PNG exporter cannot be built (PNG header file not found) ***)
    fi
  fi

#
# Test for libtiff
#

  if test -z "$LIBTIFF_LIB"; then
    AC_CHECK_LIB(tiff, TIFFReadScanline,
      [AC_CHECK_HEADER(tiffio.h,
	[TIFF='tiff'; LIBTIFF_LIB='-ltiff'],	
	)], [AC_MSG_WARN([*** TIFF exporter cannot be built (TIFF header files not found) ***])] ,  -ltiff)
  fi

if test "$PNG" = png ; then
	AC_DEFINE(HAVE_LIBPNG,1,"Define if libpng is available")
fi
if test "$TIFF" = tiff ; then
	AC_DEFINE(HAVE_LIBTIFF,1,"Define if libtiff is available")
fi

IMG_LIBS="$LIBPNG_LIB $LIBTIFF_LIB"

#
# That's a wrap!
#


AC_SUBST(GTK_CFLAGS)
AC_SUBST(GTK_LIBS)
AC_SUBST(GTKGL_CFLAGS)
AC_SUBST(GTKGL_LIBS)
AC_SUBST(IMG_LIBS)
#this is evil
#CFLAGS="$CFLAGS $GTK_CFLAGS $GL_CFLAGS $GTKGL_CFLAGS"
#LIBS="$LIBS $GTKGL_LIBS $GTK_LIBS $GL_LIBS $IMG_LIBS"


AM_GNU_GETTEXT([external])
AM_GNU_GETTEXT_VERSION([0.18])

AC_OUTPUT(Makefile src/Makefile intl/Makefile po/Makefile.in)

# end configure.in
