dnl Process this file with autoconf to produce a configure script.
dnl Created by Anjuta application wizard.

AC_INIT(fische, 3.2)

AM_INIT_AUTOMAKE(AC_PACKAGE_NAME, AC_PACKAGE_VERSION)
AC_CONFIG_HEADERS([config.h])

AC_ISC_POSIX
AC_PROG_CXX
AM_PROG_CC_STDC
AC_HEADER_STDC

AM_PROG_LIBTOOL

AC_CHECK_HEADERS(alsa/asoundlib.h pulse/simple.h portaudio.h)
AC_CHECK_LIB(asound, snd_pcm_open)
AC_CHECK_LIB(pulse-simple, pa_simple_new)
AC_CHECK_LIB(portaudio, Pa_Initialize)

PKG_CHECK_MODULES(SDL, sdl)
AC_OUTPUT([
Makefile
src/Makefile

])
