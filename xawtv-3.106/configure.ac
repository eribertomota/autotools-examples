dnl ---------------------------------------------------------------------
dnl Process this file with autoconf to produce a configure script.

AC_INIT(xawtv.spec.in)
AC_CONFIG_HEADER(config.h)


dnl ---------------------------------------------------------------------
dnl Options

AC_ARG_ENABLE(xfree-ext,
  [  --enable-xfree-ext      use XFree extentions (DGA,VidMode,DPMS)])
AC_ARG_ENABLE(xvideo,
  [  --enable-xvideo         use the Xvideo extention])
AC_ARG_ENABLE(lirc,
  [  --enable-lirc           lirc support])
AC_ARG_ENABLE(quicktime,
  [  --enable-quicktime      quicktime support])
AC_ARG_ENABLE(motif,
  [  --enable-motif          enable experimental motif support])
AC_ARG_ENABLE(aa,
  [  --enable-aa             enable aalib support])
AC_ARG_ENABLE(alsa,
  [  --enable-alsa           enable alsa support])
AC_ARG_ENABLE(zvbi,
  [  --enable-zvbi           enable vbi support (via libzvbi)])
AC_ARG_ENABLE(gl,
  [  --enable-gl             enable opengl support])
AC_ARG_ENABLE(dv,
  [  --enable-dv             enable dvlib support])
AC_ARG_ENABLE(mmx,
  [  --enable-mmx            enable mmx support])
AC_ARG_ENABLE(xft,
  [  --enable-xft            enable xft support])


dnl ---------------------------------------------------------------------
dnl Checks for programs.

AC_PROG_CC
AC_PROG_CXX
AC_PROG_CPP

AC_PROG_INSTALL
AC_CHECK_PROGS(DEPEND,gccmakedep makedepend,true)

dnl ---------------------------------------------------------------------
dnl do some OS specific stuff here

AC_HEADER_MAJOR

AC_SUBST(FOUND_AALIB)
AC_SUBST(FOUND_ALSA)
AC_SUBST(FOUND_DV)
AC_SUBST(FOUND_LQT)
AC_SUBST(FOUND_MOTIF)
AC_SUBST(FOUND_OS)
AC_SUBST(FOUND_X11)
AC_SUBST(FOUND_GL)
AC_SUBST(FOUND_ZVBI)
AC_SUBST(LIBV4L)
AC_SUBST(FOUND_EXPLAIN)
FOUND_AALIB="no"
FOUND_ALSA="no"
FOUND_DV="no"
FOUND_LQT="no"
FOUND_MOTIF="no"
FOUND_OS="unknown"
FOUND_X11="no"
FOUND_GL="no"
FOUND_ZVBI="no"
FOUND_LIRC="no"
LIBV4L="no"
FOUND_EXPLAIN="no"

case "`uname -s`" in
	Linux)
		FOUND_OS="linux"
		;;
	OpenBSD | FreeBSD | NetBSD)
		# *BSD has important stuff (from ports)
		# in /usr/local ...
		CFLAGS="$CFLAGS -I/usr/local/include -L/usr/local/lib"
		LDLIBS="$LDLIBS -L/usr/local/lib"
		FOUND_OS="bsd"
		;;
	GNU/kFreeBSD)
		FOUND_OS="bsd"
		;;
	*)
		AC_MSG_CHECKING(if xawtv will build on `uname -s`)
		AC_MSG_RESULT(maybe)
		FOUND_OS="unknown"
		;;
esac


dnl ---------------------------------------------------------------------
dnl Checks for functions

AC_EGREP_HEADER(sockaddr_storage,sys/socket.h,AC_DEFINE(HAVE_SOCKADDR_STORAGE,1,"have ipv6"))
AC_CHECK_HEADERS(getopt.h soundcard.h unistd.h sys/select.h sys/soundcard.h alsa/asoundlib.h linux/joystick.h dev/ic/bt8xx.h machine/ioctl_bt848.h)
AC_CHECK_FUNCS(ftello fseeko getpt getnameinfo getopt_long strcasestr dlopen)

AC_SUBST(DLFLAGS)
DLFLAGS=""
if test "$ac_cv_func_dlopen" = "no"; then
  AC_CHECK_LIB(dl,dlopen, [ DLFLAGS="-ldl" ] )
fi
AC_MSG_CHECKING(for ELF)
if test -z "`echo __ELF__ | $CC -E - | grep __ELF__`"; then
  AC_MSG_RESULT(yes)
  DLFLAGS="$DLFLAGS -Wl,-E"
else
  AC_MSG_RESULT(no)
fi

AC_CHECK_LIB(pthread,pthread_create,LIBPTHREAD="-lpthread")
if test "$LIBPTHREAD" = ""; then
  AC_CHECK_LIB(c_r,pthread_create,LIBPTHREAD="-lc_r")
fi
AC_CHECK_LIB(ossaudio,main,LIBOSS="-lossaudio")
AC_CHECK_LIB(ncursesw,initscr,LIBCURSES="-lncursesw")
if test "$LIBCURSES" = ""; then
  AC_CHECK_LIB(ncurses,initscr,LIBCURSES="-lncurses")
fi
if test "$LIBCURSES" = ""; then
  AC_CHECK_LIB(curses,initscr,LIBCURSES="-lcurses")
fi
if test "$LIBCURSES" = ""; then
  echo "Oops: (n)curses library not found.  You need this one, please install."
  echo "Note: to compile stuff just the library packages are not enougth,"
  echo "      you need also the *-devel packages."
  exit 1
fi
if test "$LIBCURSES" = "-lncursesw"; then
  CFLAGS="$CFLAGS -I/usr/include/ncursesw"
fi
AC_SUBST(LIBPTHREAD)
AC_SUBST(LIBOSS)
AC_SUBST(LIBCURSES)


dnl ---------------------------------------------------------------------
dnl X11 checks

AC_PATH_XTRA
if test "$no_x" != "yes"; then
  FOUND_X11="yes"
  ATHENA="-lXaw -lXmu -lXt $X_PRE_LIBS -lXpm -lXext -lX11 $X_EXTRA_LIBS"
  XFT_FLAGS=""
  XFT_LIBS=""
  if test "$enable_xft" != "no"; then
    AC_MSG_CHECKING(for Xft)
    if test -x "`which pkg-config 2>/dev/null`" && pkg-config xft && pkg-config fontconfig; then
      XFT_FLAGS="`pkg-config --cflags xft fontconfig`"
      XFT_LIBS="`pkg-config --libs xft fontconfig`"
      AC_DEFINE(HAVE_XFT,1,"have xft")
      AC_MSG_RESULT(yes)
    else
      AC_MSG_RESULT(no)
    fi
  fi
else
  ATHENA=""
fi
AC_SUBST(X_CFLAGS)
AC_SUBST(X_PRE_LIBS)
AC_SUBST(X_EXTRA_LIBS)
AC_SUBST(X_LIBS)
AC_SUBST(x_includes)
AC_SUBST(ATHENA)
AC_SUBST(SUBS)
AC_SUBST(TOOLS)
AC_SUBST(LDLIBS)
AC_SUBST(XFT_FLAGS)
AC_SUBST(XFT_LIBS)

AC_CHECK_LIB(v4l2, v4l2_fd_open, LIBV4L="yes",,)
if test "$LIBV4L" != "yes"; then
    echo "Oops:	libv4l library not found. This is needed to use most webcams."
    echo "Note:	to compile stuff just the library packages are not enough,"
    echo "	you need also the *-devel packages."
fi

AC_CHECK_LIB(explain, explain_open, 
	 AC_DEFINE(HAVE_EXPLAIN,1,"have libexplain") FOUND_EXPLAIN="yes",,)


AC_CHECK_LIB(jpeg, jpeg_start_compress, JPEG="found",,)
if test "$JPEG" != "found"; then
    echo "Oops:	jpeg library not found.  You need this one, please install."
    echo "Note:	to compile stuff just the library packages are not enougth,"
    echo "	you need also the *-devel packages."
    exit 1
fi

AC_SUBST(LIBALSA)
LIBALSA=""
if test "$enable_alsa" != "no"; then
    AC_CHECK_LIB(asound, snd_seq_open,
	AC_DEFINE(HAVE_ALSA,1,"have alsa") FOUND_ALSA="yes"; LIBALSA="-lasound",,)
else
    echo "*** alsa disabled"
fi

AC_SUBST(LIRC)
LIRC=""
if test "$enable_lirc" != "no"; then
    AC_CHECK_LIB(lirc_client, lirc_init,
	AC_DEFINE(HAVE_LIBLIRC_CLIENT,1,"have lirc") FOUND_LIRC="yes"; LIRC="-llirc_client",,)
else
    echo "*** lirc disabled"
fi

AC_SUBST(LIBZVBI)
LIBZVBI=""
if test "$enable_zvbi" != "no"; then
    AC_CHECK_LIB(zvbi, vbi_capture_fd,
	AC_DEFINE(HAVE_ZVBI,1,"have zvbi") FOUND_ZVBI="yes"; LIBZVBI="-lzvbi -lpthread -lm -lpng -lz",,$LIBPTHREAD)
else
    echo "*** zvbi disabled"
fi

AC_SUBST(AALIBS)
AALIBS=""
if test "$enable_aa" != "no"; then
    AC_CHECK_LIB(aa,aa_autoinit, [ FOUND_AALIB="yes" ],,)
    if test "$FOUND_AALIB" = "yes"; then
	AALIBS=-laa
	if test -x "`which aalib-config 2>/dev/null`"; then
	    AALIBS=`aalib-config --libs`
	fi
    fi
else
    echo "*** aalib support disabled"
fi

AC_SUBST(LIBDV)
LIBDV=""
if test "$enable_dv" != "no"; then
    AC_CHECK_LIB(dv, dv_decoder_new,
	AC_DEFINE(HAVE_DV,1,"have dv") FOUND_DV="yes"; LIBDV="-ldv -lm",,
		-lm $LIBPTHREAD)
else
    echo "*** DV disabled"
fi

dashlglib=$(pkg-config glib-2.0 --libs 2>/dev/null)
if test "$dashlglib" = ""; then
	dashlglib=$(glib-config --libs 2>/dev/null)
fi
if test "$enable_quicktime" != "no"; then
    AC_CHECK_LIB(quicktime, lqt_query_registry,
	FOUND_LQT="yes"; AC_DEFINE(HAVE_LIBQUICKTIME,1,"have libquicktime"),,
	$DLFLAGS $dashlglib $LIBPTHREAD)
else
    echo "*** quicktime disabled"
fi
QTLIBS=""
if test "$FOUND_LQT" = "yes"; then
    QTFLAGS="`pkg-config libquicktime --cflags-only-I`"
    if test "$QTFLAGS" = ""; then
	QTFLAGS= "-I/usr/include/quicktime"
    fi
    QTLIBS="-lquicktime $DLFLAGS $dashlglib -lm"
fi
AC_SUBST(QTLIBS)
AC_SUBST(QTFLAGS)

if test "$enable_xfree_ext" != "no"; then
    AC_CHECK_LIB(Xxf86dga, XF86DGAQueryExtension,,,
	$X_LIBS $X_PRE_LIBS -lXext -lX11 $X_EXTRA_LIBS)
    AC_CHECK_LIB(Xxf86vm, XF86VidModeQueryExtension,,,
	$X_LIBS $X_PRE_LIBS -lXext -lX11 $X_EXTRA_LIBS)
    AC_CHECK_LIB(Xdpms, DPMSQueryExtension,,,
	$X_LIBS $X_PRE_LIBS -lXext -lX11 $X_EXTRA_LIBS)
    if test "$ac_cv_lib_Xdpms_DPMSQueryExtension" = "no"; then
	AC_CHECK_LIB(Xext, DPMSQueryExtension,AC_DEFINE(HAVE_LIBXDPMS),,
	    $X_LIBS $X_PRE_LIBS -lXext -lX11 $X_EXTRA_LIBS)
    fi
    AC_CHECK_LIB(Xinerama, XineramaQueryExtension,,,
	$X_LIBS $X_PRE_LIBS -lXext -lX11 $X_EXTRA_LIBS)
    AC_CHECK_LIB(Xrender, XRenderQueryExtension,,,
	$X_LIBS $X_PRE_LIBS -lXext -lX11 $X_EXTRA_LIBS)
    AC_CHECK_LIB(Xrandr, XRRConfigCurrentConfiguration,,,
	$X_LIBS $X_PRE_LIBS -lXext -lX11 $X_EXTRA_LIBS)
else
    echo "*** XFree extentions disabled"
fi

if test "$enable_xvideo" != "no"; then
    AC_CHECK_LIB(Xv, XvQueryExtension,,,
	$X_LIBS $X_PRE_LIBS -lXext -lX11 $X_EXTRA_LIBS)
else
    echo "*** Xvideo extention disabled"
fi

if test "$enable_motif" != "no"; then
    AC_CHECK_LIB(Xm,XmStringGenerate, [ FOUND_MOTIF="yes" ],,
	$X_LIBS $X_PRE_LIBS -lXext -lX11 $X_EXTRA_LIBS)
else
    echo "*** motif support disabled"
fi

AC_SUBST(LIBGL)
LIBGL=""
if test "$enable_gl" != "no"; then
    AC_CHECK_LIB(GL, glXChooseVisual,
	AC_DEFINE(HAVE_GL,1,"have opengl") FOUND_GL="yes"; LIBGL="-lGL -lm",,
	$X_LIBS $X_PRE_LIBS -lXext -lX11 $X_EXTRA_LIBS -lm)
else
    echo "*** OpenGL disabled"
fi

VERSION="`head -1 $srcdir/Changes`"
AC_SUBST(VERSION)

dnl ---------------------------------------------------------------------
AC_MSG_CHECKING(for X11 config directory)
x11conf=/usr/lib/X11
if test -d /etc/X11; then
	x11conf=/etc/X11
fi
AC_MSG_RESULT($x11conf)
AC_SUBST(x11conf)

AC_MSG_CHECKING(for X11 app-defaults directory)
resdir=/usr/lib/X11
if test -d /usr/share/X11/app-defaults; then
	resdir=/usr/share/X11
fi
if test -d /etc/X11/app-defaults; then
	resdir=/etc/X11
fi
AC_MSG_RESULT($resdir/app-defaults)
AC_SUBST(resdir)

dnl ---------------------------------------------------------------------
dnl for screenlock
AC_DEFINE(HAVE_XMU,1,"have xmu")

dnl ---------------------------------------------------------------------
dnl deinterlace plugins
AC_MSG_CHECKING(if mmx should be used)
AC_SUBST(USE_MMX)
if test "$enable_mmx" = "no" -o "$enable_mmx" = "yes"; then
	USE_MMX="$enable_mmx"
else
	case "`uname -m`" in
		i586 | i686)
			USE_MMX="yes"
			;;
		*)
			USE_MMX="no"
			;;
	esac
fi
AC_MSG_RESULT($USE_MMX)

dnl ---------------------------------------------------------------------
AC_OUTPUT(Makefile xawtv.spec)
for dir in \
	common console debug fonts jwz libvbi vbistuff x11 structs \
	libng libng/plugins libng/contrib-plugins mk
do
	test -d $dir && continue
	mkdir -p $dir
done

dnl ---------------------------------------------------------------------
dnl compile time options summary

cat <<EOF

compile time options summary
============================

    aalib        : $FOUND_AALIB
    alsa         : $FOUND_ALSA
    dv           : $FOUND_DV
    QuickTime    : $FOUND_LQT
    OpenMotif    : $FOUND_MOTIF
    X11R6        : $FOUND_X11
    OpenGL       : $FOUND_GL
    zvbi         : $FOUND_ZVBI
    libv4l       : $LIBV4L
    libexplain   : $FOUND_EXPLAIN
    lirc         : $FOUND_LIRC

EOF
