AC_INIT([videotrans], [1.6.1], [videotrans@berkvens.net], [videotrans])
AC_PREREQ([2.53])
AC_REVISION([$Version:$])
AC_CONFIG_SRCDIR([aspects.txt])
AC_CONFIG_AUX_DIR([ac-support])

AC_PROG_INSTALL

[videotrans_warnings=""]
AC_CHECK_PROG([MPLAYER], [mplayer], [yes], [no])
if test x$MPLAYER = xno ; then AC_MSG_ERROR([mplayer is required, please get it from http://www.mplayerhq.hu/]) ; fi
[mplayer_version="`mplayer | head -1 | sed 's,^[^ ]* \([^- ]*\).*,\1,'`"]
if test x$mplayer_version != x1.0pre7try2 ; then if test x$mplayer_version != x1.0rc1 ; then if test x$mplayer_version != x1.0rc4 ; then AC_MSG_WARN([This program is known to work correctly with mplayer version 1.0pre7try2, 1.0rc1 and 1.0rc4. Your mplayer version is $mplayer_version, which might not work correctly and even crash during conversion. Please consider upgrading mplayer if it is older than 1.0pre7try2. If your mplayer is newer than 1.0rc4 and crashes during conversion, please consider downgrading it to 1.0rc4.]) ; [videotrans_warnings="$videotrans_warnings This program is known to work correctly with mplayer version 1.0pre7try2 and 1.0rc1. Your mplayer version is $mplayer_version, which might not work correctly and even crash during conversion. Please consider upgrading mplayer if it is older than 1.0pre7try2. If your mplayer is newer than 1.0rc1 and crashes during conversion, please consider downgrading it to 1.0rc1."] ; fi ; fi ; fi
AC_CHECK_PROG([FFMPEG], [ffmpeg], [yes], [no])
if test x$FFMPEG = xno ; then AC_MSG_ERROR([ffmpeg is required, please get it from http://ffmpeg.sourceforge.net/]) ; fi
AC_CHECK_PROG([MPEG2ENC], [mpeg2enc], [yes], [no])
if test x$MPEG2ENC = xno ; then AC_MSG_ERROR([mpeg2enc is required, please get it from http://mjpeg.sourceforge.net/]) ; fi
AC_CHECK_PROG([MP2ENC], [mp2enc], [yes], [no])
if test x$MP2ENC = xno ; then AC_MSG_ERROR([mp2enc is required, please get it from http://mjpeg.sourceforge.net/]) ; fi
AC_CHECK_PROG([PNG2YUV], [png2yuv], [yes], [no])
if test x$PNG2YUV = xno ; then AC_MSG_ERROR([png2yuv is required, please get it from http://mjpeg.sourceforge.net/]) ; fi
AC_CHECK_PROG([JPEG2YUV], [jpeg2yuv], [yes], [no])
if test x$JPEG2YUV = xno ; then AC_MSG_ERROR([jpeg2yuv is required, please get it from http://mjpeg.sourceforge.net/]) ; fi
AC_CHECK_PROG([CONVERT], [convert], [yes], [no])
if test x$CONVERT = xno ; then AC_MSG_ERROR([convert is required, please get it from http://www.imagemagick.org/]) ; fi
AC_CHECK_PROG([IDENTIFY], [identify], [yes], [no])
if test x$IDENTIFY = xno ; then AC_MSG_ERROR([identify is required, please get it from http://www.imagemagick.org/]) ; fi
AC_CHECK_PROG([SPUMUX], [spumux], [yes], [no])
if test x$SPUMUX = xno ; then AC_MSG_ERROR([spumux is required, please get it from http://dvdauthor.sourceforge.net/]) ; fi

AC_PROG_MAKE_SET
AC_CONFIG_FILES(Makefile)
AC_CONFIG_SUBDIRS(src man1 data)
AC_OUTPUT

[if test "x$videotrans_warnings" = x ; then true ; else echo ; echo "WARNING: $videotrans_warnings" >&2 ; fi]

[true]
