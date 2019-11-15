#################################
# Initialize Autoconf
AC_PREREQ([2.60])
AC_INIT([Gesture Recognition And Instantiation Library],
        [3.1.1],
        [],
        [grail])
AC_CONFIG_SRCDIR([Makefile.am])
AC_CONFIG_HEADERS([config.h])
AC_CONFIG_AUX_DIR([config-aux])
AC_CONFIG_MACRO_DIR([m4])

#################################
# Initialize Automake
AM_INIT_AUTOMAKE([foreign dist-bzip2])
AM_SILENT_RULES([yes])
AM_MAINTAINER_MODE([enable])

LIB_VERSION=6:0:0
AC_SUBST([LIB_VERSION])

# Initialize libtool
AC_PROG_LIBTOOL

#################################
# Checks for programs.
AC_PROG_CC
AC_PROG_CXX
AC_PROG_INSTALL

#################################
# Enable/disable X11 support

AC_ARG_WITH(x11,
            AC_HELP_STRING(--without-x11, Do not use X11 libraries or frame_x11.h (default: autodetect)),
            [],
            [with_x11=auto])

AS_IF([test "x$with_x11" = "xauto"],
      [
        PKG_CHECK_MODULES(XINPUT,
                          frame-x11 x11 xext [xi >= 1.5.99.1] [inputproto >= 2.1.99.6],
                          [have_xinput=yes],
                          [have_xinput=no])
      ])

AS_IF([test "x$with_x11" = "xyes"],
      [
        PKG_CHECK_MODULES(XINPUT,
                          frame-x11 x11 xext [xi >= 1.5.99.1] [inputproto >= 2.1.99.6],
                          [have_xinput=yes])
      ])

AS_IF([test "x$with_x11" = "xno"],
      [have_xinput=no])

AS_IF([test "x$have_xinput" = "xyes"],
      [
        AM_CONDITIONAL(HAVE_XINPUT, true)
      ],
      [
        AM_CONDITIONAL(HAVE_XINPUT, false)
      ])

#################################
# check mandatory build dependencies

PKG_CHECK_MODULES([FRAME], [frame >= 2.5.0])

#################################
# debug builds

AC_ARG_ENABLE(debug,
              AC_HELP_STRING(--enable-debug, Enable debug assertions and other safeguards (default: disabled)),
              [],
              AC_DEFINE([NDEBUG], [], [No debug]))

#################################
# Check for TDD tools
AC_ARG_ENABLE([integration-tests],
              [AS_HELP_STRING([--enable-integration-tests],
                  [Enable building integration test cases (default: auto)])],
              [enable_integration_tests=$enableval],
              [enable_integration_tests=auto])

#################################
# Check for Google C++ Testing Framework
CHECK_GTEST()
AM_CONDITIONAL([HAVE_GTEST], [test "x$have_gtest" = xyes])

AS_IF([test "x$enable_integration_tests" != xno],
      [CHECK_XORG_GTEST(
          [AC_MSG_NOTICE([xorg-gtest is available, integration tests will be built])],
          [AS_IF([test "x$enable_integration_tests" = xyes],
                 [AC_MSG_ERROR(
                     [xorg-gtest is not available])],
                 [AC_MSG_WARN(
                     [xorg-gtest is not available, tests will not be built])
                  have_xorg_gtest=no])])])

AM_CONDITIONAL([ENABLE_INTEGRATION_TESTS], [test "x$have_xorg_gtest" = xyes])
                 
#################################
# Enable coverage reports using gcov
AC_TDD_GCOV

AM_CONDITIONAL([HAVE_GCOV],[test "x$ac_cv_check_gcov" = xyes])
 
AC_CONFIG_FILES([Makefile
                 src/Makefile
                 tools/Makefile
                 test/Makefile
                 test/gtest/Makefile
                 test/integration/Makefile
                 test/regular/Makefile
                 grail.pc])

AC_SUBST(VISIBILITY_CFLAGS, "-fvisibility=hidden")
AC_SUBST(VISIBILITY_CXXFLAGS, "-fvisibility=hidden")
AC_SUBST(WARNING_CPPFLAGS, "-Wall -Werror")
AC_SUBST(CXX11_CXXFLAGS, "-std=c++0x")

AC_OUTPUT

#################################
# Print summary

bold_green=$(tput bold)$(tput setf 2)
bold_white=$(tput bold)$(tput setf 7)
reset=$(tput sgr0)

AC_MSG_NOTICE([])
AC_MSG_NOTICE([${bold_green}Open Input Framework - Grail library - $VERSION${reset}])
AC_MSG_NOTICE([])
AC_MSG_NOTICE([   Prefix                  : ${bold_white}${prefix}${reset}])
AC_MSG_NOTICE([   CFLAGS                  : ${bold_white}${CFLAGS} ${GCC_FLAGS}${reset}])
AC_MSG_NOTICE([   X11 support             : ${bold_white}${have_xinput}${reset}])
AC_MSG_NOTICE([   Build integration tests : ${bold_white}${have_xorg_gtest}${reset}])
AC_MSG_NOTICE([])
