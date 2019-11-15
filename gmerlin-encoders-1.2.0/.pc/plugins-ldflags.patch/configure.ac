AC_INIT
AC_CONFIG_SRCDIR([include/gmerlin_encoders.h])

AM_CONFIG_HEADER(include/config.h)
AM_INIT_AUTOMAKE(gmerlin-encoders, 1.2.0)

SAVE_CFLAGS=$CFLAGS
AC_DISABLE_STATIC
AC_PROG_LIBTOOL

CFLAGS=$SAVE_CFLAGS

dnl
dnl Check for Dependencies package
dnl

GMERLIN_DEP_DIR=/opt/gmerlin

if test -d $GMERLIN_DEP_DIR; then
  have_opt_gmerlin="true"
  export PKG_CONFIG_PATH=$GMERLIN_DEP_DIR/lib/pkgconfig:$PKG_CONFIG_PATH
  GMERLIN_DEP_CFLAGS="-I$GMERLIN_DEP_DIR/include"
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

LDFLAGS=$GMERLIN_DEP_RPATH
AC_SUBST(GMERLIN_DEP_LIBS)
AC_SUBST(GMERLIN_DEP_CFLAGS)

dnl
dnl Required libraries
dnl

GMERLIN_REQUIRED="1.2.0"
PKG_CHECK_MODULES(GMERLIN, gmerlin >= $GMERLIN_REQUIRED, , AC_MSG_ERROR("gmerlin not found"))

gmerlin_plugindir='$(libdir)/gmerlin/plugins'

dnl LDFLAGS for plugins
GMERLIN_PLUGIN_LDFLAGS="-export-symbols "`pkg-config --variable=prefix gmerlin`"/share/gmerlin/plugin.sym"

AC_SUBST(GMERLIN_PLUGIN_LDFLAGS)
AC_SUBST(gmerlin_plugindir)
AC_SUBST(GMERLIN_REQUIRED)

AM_GNU_GETTEXT([external])

dnl
dnl Optional libraries
dnl

dnl
dnl Ogg
dnl

GMERLIN_CHECK_OGG

dnl
dnl Vorbis
dnl

GMERLIN_CHECK_VORBIS

dnl
dnl Theora
dnl

GMERLIN_CHECK_THEORAENC
GMERLIN_CHECK_THEORADEC

dnl
dnl Speex
dnl

GMERLIN_CHECK_SPEEX

dnl
dnl FLAC
dnl

GMERLIN_CHECK_FLAC
 
dnl
dnl lame
dnl

GMERLIN_CHECK_LAME

dnl
dnl faac
dnl

GMERLIN_CHECK_FAAC

dnl
dnl mjpegtools
dnl

GMERLIN_CHECK_MJPEGTOOLS

dnl
dnl libavcodec
dnl

GMERLIN_CHECK_AVCODEC

dnl
dnl libavformat
dnl

GMERLIN_CHECK_AVFORMAT

dnl
dnl libshout
dnl

GMERLIN_CHECK_SHOUT

dnl
dnl CFLAGS
dnl

LQT_OPT_CFLAGS($host_cpu, ["-O3 -funroll-all-loops -fomit-frame-pointer -ffast-math"])

CFLAGS="$CFLAGS -D_REENTRANT -D_FILE_OFFSET_BITS=64 $OPT_CFLAGS $GMERLIN_CFLAGS"

LQT_TRY_CFLAGS(-Wall, CFLAGS="$CFLAGS -Wall")
LQT_TRY_CFLAGS(-Wmissing-declarations, CFLAGS="$CFLAGS -Wmissing-declarations" )
LQT_TRY_CFLAGS(-Wdeclaration-after-statement, CFLAGS="$CFLAGS -Wdeclaration-after-statement")


dnl
dnl LIBS
dnl

LIBS="$GMERLIN_LIBS"

if test "x$prefix" = xNONE; then
   prefix="${ac_default_prefix}"
fi
if test "x$exec_prefix" = xNONE; then
   exec_prefix="${prefix}"
fi

AC_CONFIG_FILES([Makefile \
po/Makefile.in \
gmerlin_encoders.spec \
include/Makefile \
lib/Makefile \
m4/Makefile \
utils/Makefile \
plugins/Makefile \
plugins/flac/Makefile \
plugins/ogg/Makefile \
plugins/lame/Makefile \
plugins/faac/Makefile \
plugins/yuv4mpeg/Makefile \
plugins/ffmpeg/Makefile \
])

AC_OUTPUT

echo ""
echo "=== Libraries: ================================="

echo -n "flac:       "
if test "x$have_flac" = "xtrue"; then
echo "Found (CFLAGS=$FLAC_CFLAGS LIBS=$FLAC_LIBS)"
else
echo "Missing (Go to: http://flac.sourceforge.net/)"
fi

echo -n "ogg:        "
if test "x$have_ogg" = "xtrue"; then
echo "Found (CFLAGS=$OGG_CFLAGS LIBS=$OGG_LIBS)"
else
echo "Missing (Go to: http://www.xiph.org/)"
fi

echo -n "vorbis:     "
if test "x$have_vorbis" = "xtrue"; then
echo "Found (CFLAGS=$VORBIS_CFLAGS LIBS=$VORBIS_LIBS)"
else
echo "Missing (Go to: http://www.vorbis.com/)"
fi

echo -n "theoraenc:  "
if test "x$have_theoraenc" = "xtrue"; then
echo "Found (CFLAGS=$THEORAENC_CFLAGS LIBS=$THEORAENC_LIBS)"
else
echo "Missing (Go to: http://www.theora.org/)"
fi

echo -n "speex:      "
if test "x$have_speex" = "xtrue"; then
echo "Found (CFLAGS=$SPEEX_CFLAGS LIBS=$SPEEX_LIBS)"
else
echo "Missing (Go to: http://www.speex.org/)"
fi

echo -n "lame:       "
if test "x$have_lame" = "xtrue"; then
echo "Found (CFLAGS=$LAME_CFLAGS LIBS=$LAME_LIBS)"
else
echo "Missing (Go to: http://www.mp3dev.org/)"
fi

echo -n "faac:       "
if test "x$have_faac" = "xtrue"; then
echo "Found (CFLAGS=$FAAC_CFLAGS LIBS=$FAAC_LIBS)"
else
echo "Missing (Go to: http://www.audiocoding.com/)"
fi

echo -n "mjpegtools: "
if test "x$have_mjpegtools" = "xtrue"; then
echo "Found (CFLAGS=$MJPEGTOOLS_CFLAGS LIBS=$MJPEGTOOLS_LIBS)"
else
echo "Missing (Go to: http://mjpeg.sourceforge.net/)"
fi

echo -n "ffmpeg:     "
if test "x$have_avformat" = "xtrue"; then
echo "Found (CFLAGS=$AVFORMAT_CFLAGS LIBS=$AVFORMAT_LIBS)"
else
echo "Missing (Go to: http://ffmpeg.org/)"
fi

echo -n "libshout:   "
if test "x$have_shout" = "xtrue"; then
echo "Found (CFLAGS=$SHOUT_CFLAGS LIBS=$SHOUT_LIBS)"
else
echo "Missing (Go to: http://icecast.org/)"
fi


echo
echo "If you installed a library but it was not detected, check the file INSTALL"
echo "for troubleshooting tips. Also note that if the configure script reaches"
echo "this point, all missing packages are optional so compilation should succeed"
echo "anyway."
