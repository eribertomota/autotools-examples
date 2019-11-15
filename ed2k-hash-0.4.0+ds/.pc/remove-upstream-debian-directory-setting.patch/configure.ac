dnl ==============================================================
dnl Process this file with autoconf to produce a configure script.
dnl (or run ./autogen.sh if it exists)
dnl ==============================================================

AC_INIT(ed2k_hash/processfile.h)

AM_INIT_AUTOMAKE(ed2k_hash,0.4.0)

dnl This ksh/zsh feature conflicts with `cd blah ; pwd`
unset CDPATH

AC_PROG_CC
AC_PROG_CXX

AC_PREFIX_DEFAULT(/usr/local)

AM_CONFIG_HEADER(config.h)

AC_LANG_CPLUSPLUS

dnl ==============================================================
dnl Check for the FLTK toolkit.
dnl
dnl Sometimes header files are like FL/Fl_Window.h, and
dnl sometimes they are like FL/Fl_Window.H. Unfortunately,
dnl this is not straight-forward to distinguish with the
dnl test result defines in config.h, as they all get 
dnl capitalised.
dnl 
dnl So we have to define our own: HAVE_FL_WITH_LC_H 
dnl ==============================================================

want_fltk_gui=no
have_fltk_headers=no 

AC_CHECK_LIB(fltk,main,[have_fltk_libs=yes],[have_fltk_libs=no])

AC_CHECK_HEADERS([FL/Fl.h],[
  AC_DEFINE(HAVE_FL_WITH_LC_H,,[The .h in FL/Fl_foo.h is lower case, not upper case])
  have_fltk_headers=yes
])

AC_CHECK_HEADERS([FL/Fl_Window.H], [
  AC_DEFINE(HAVE_FL_WITH_UC_H,,[The .H in FL/Fl_foo.H is upper case, not lower case])
  have_fltk_headers=yes
])

if test "x$have_fltk_headers" == "xyes"
then
  if test "x$have_fltk_libs" == "xyes"
  then
    want_fltk_gui=yes
  fi
fi

AM_CONDITIONAL([FLTK_OPT], [ test "x$want_fltk_gui" == "xyes" ])

dnl ===========================
dnl output Makefiles
dnl ===========================

AC_OUTPUT([
./Makefile
debian/Makefile
ed2k_hash/Makefile
ed2k_hash/docs/Makefile
ed2k_hash/docs/en/Makefile
ed2k_hash/GUI/Makefile
])


