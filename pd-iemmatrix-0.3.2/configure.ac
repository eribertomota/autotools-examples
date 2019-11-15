dnl Process this file with autoconf to produce a configure script.
AC_PREREQ([2.60])

AC_INIT([iemmatrix], [0.3.2], [zmoelnig@iem.at], [iemmatrix], [https://git.iem.at/pd/iemmatrix])
AM_INIT_AUTOMAKE([1.10 foreign])
m4_ifdef([LT_INIT], 
	[LT_INIT([disable-static win32-dll])],
	[AC_ENABLE_SHARED
	 AC_DISABLE_STATIC
	 AC_LIBTOOL_WIN32_DLL])

AC_CONFIG_MACRO_DIR([m4])

AC_CONFIG_HEADERS([config.h])
AC_CONFIG_FILES([Makefile])
AC_CONFIG_FILES([doc/Makefile abs/Makefile])
AC_CONFIG_FILES([iemmatrix-meta.pd])
AC_CONFIG_FILES([VERSION.txt])

AC_CONFIG_SRCDIR([src/iemmatrix.c])

IEM_OPERATING_SYSTEM
ARCH=$(uname -m)
KERN=$(uname -s)

dnl m4_ifdef([AC_LIB_RPATH], [AC_LIB_RPATH])

dnl Checks for programs.
AC_PROG_CC
AC_PROG_LN_S
AC_LIBTOOL_WIN32_DLL
AC_PROG_LIBTOOL

AC_ARG_WITH([pd],
            AC_HELP_STRING([--with-pd=</path/to/pd>],
                           [where to look for Pd-headers and and -libs]))
AC_ARG_WITH([extension],
            AC_HELP_STRING([--with-extension=<ext>],
                           [enforce a certain extension for the dynamic library (e.g. dll)]))
AC_ARG_ENABLE([library],
            AC_HELP_STRING([--enable-library],
                           [build iemmatrix as multi-object library (default, "yes"), as single-object externals ("no") or as both ("both")]))
AC_ARG_WITH([build-date],
            AC_HELP_STRING([--with-build-date=<str>],
                           [alternative date string]))

AM_CONDITIONAL([LIBRARY], [test "x${enable_library}" != "xno"])
AM_CONDITIONAL([SINGLEOBJECTS], [test "x${enable_library}" = "xno" || test "x${enable_library}" = "xboth"])


if test "x${libdir}" = "x\${exec_prefix}/lib"; then
 libdir='${exec_prefix}/lib/pd/extra'
fi


if test "x$with_pd" != "x"; then
 if test -d "${with_pd}"; then
   PDPATH=${with_pd}
 fi
 if test -d "${PDPATH}/src"; then
  AC_MSG_RESULT([adding ${PDPATH}/src to CPPFLAGS])
  CPPFLAGS="-I${PDPATH}/src ${CPPFLAGS}"

  AC_MSG_RESULT([adding ${PDPATH}/src to LDFLAGS])
  LDFLAGS="-L${PDPATH}/src ${LDFLAGS}"
 else
  if test -d "${PDPATH}"; then
   AC_MSG_RESULT([adding ${PDPATH} to CPPFLAGS])
   CPPFLAGS="-I${PDPATH} ${CPPFLAGS}"
  fi
 fi
 if test -d "${PDPATH}/bin"; then
  AC_MSG_RESULT([adding ${PDPATH}/bin to LDFLAGS])
  LDFLAGS="-L${PDPATH}/bin ${LDFLAGS}"
 else
  if test -d "${PDPATH}"; then
   AC_MSG_RESULT([adding ${PDPATH} to LDFLAGS])
   LDFLAGS="-L${PDPATH} ${LDFLAGS}"
  fi
 fi
fi

dnl Checks for libraries.
dnl Replace `main' with a function in -lc:
AC_CHECK_LIB([c], [main])

dnl Replace `main' with a function in -lm:
AC_CHECK_LIB([m], [cos])
dnl for math.h Bessel/Neumann functions
AC_CHECK_LIB([m], [jn])
AS_IF([test "xyes" = "x${ac_cv_lib_m_jn}"],[
   AC_DEFINE(HAVE_MATH_BESSEL,1,[can math compute Bessel functions?])
])
AM_CONDITIONAL(HAVE_MATH_BESSEL, [test "x${ac_cv_lib_m_jn}" = "xyes"])


dnl Replace `main' with a function in -lpthread:
dnl AC_CHECK_LIB([pthread], [main])
dnl Replace `main' with a function in -lstk:
dnl AC_CHECK_LIB([stk], [main], [STK=yes])

tmp_pddll_LIBS=$LIBS
AC_CHECK_LIB([:pd.dll], [nullfn], [have_pddll="yes"], [have_pddll="no"])
LIBS=$tmp_pddll_LIBS

AS_IF([test "x$have_pddll" = "xyes"],[
  EXTRA_LTFLAGS="$EXTRA_LTFLAGS -Xlinker -l:pd.dll"
  ],[
  AC_CHECK_LIB([pd], [nullfn])
])

dnl Checks for header files.
AC_HEADER_STDC
AC_CHECK_HEADERS([io.h math.h memory.h stdio.h stdlib.h string.h unistd.h])

dnl Checks for typedefs, structures, and compiler characteristics.
AC_HEADER_TIME

dnl Checks for library functions.
AC_FUNC_MMAP

IEM_CHECK_FAT(ARCH_FLAG)

IEM_CHECK_CFLAGS([-mms-bitfields])
IEM_CHECK_SIMD

AC_MSG_CHECKING([extension])
if test "x$with_extension" != "x"
then
 EXTENSION=$with_extension
else
 case "$KERN" in
 Darwin)
   EXTENSION=pd_darwin
   ;;
 Linux)
   EXTENSION=pd_linux
   ;;
 IRIX64)
   EXTENSION=pd_irix6
   ;;
 IRIX32)
   EXTENSION=pd_irix5
   ;;
 IRIX64)
   EXTENSION=pd_irix6
   ;;
 *CYGWIN*)
   EXTENSION=dll
   ;;
 *MINGW*)
   EXTENSION=dll
   ;;
 *)
   EXTENSION=pd_linux
   ;;
 esac
fi
AC_MSG_RESULT([$EXTENSION])

have_pd="no"
AC_CHECK_HEADERS([pd/m_pd.h m_pd.h], [have_pd="yes"])
AS_IF([test "x${have_pd}" = "xno"],[
AC_ERROR([m_pd.h is desperately needed!
        install pd and/or use
        "--with-pd=</path/to/pd/>"])
])

AC_ARG_WITH([fftw], AC_HELP_STRING([--without-fftw], [compile without FFTW]))
AS_IF([test "xno" != "x${with_fftw}" ],[
have_fftw="no"
have_fftw3="no"
AC_CHECK_LIB([fftw3],[fftw_execute])
  AS_IF([test "x$ac_cv_lib_fftw3_fftw_execute" != "xyes"],[
      AC_CHECK_LIB([fftw3-3],[fftw_execute])
      ac_cv_lib_fftw3_fftw_execute=$ac_cv_lib_fftw3_3_fftw_execute
  ])
  AS_IF([test "x$ac_cv_lib_fftw3_fftw_execute" = "xyes"],[
      AC_CHECK_HEADERS([fftw3.h], [have_fftw3="yes"])
  ])
])
AS_IF([test "xyes" = "x${have_fftw3}"],[
   have_fftw="yes"
   AC_DEFINE(HAVE_LIBFFTW3, 1, [Define to 1 if you have the 'fftw3' library (-lfftw3).])
])
AS_IF([test "xyes" = "x${have_fftw}" ],[
dnl   AC_DEFINE(HAVE_LIBFFTW,1,[Define to 1 if you have the 'fftw' library (e.g. -lfftw3).])
   AC_DEFINE(USE_FFTW, 1, [can we use fftw?])
])

AM_CONDITIONAL(HAVE_FFTW, [test "x${have_fftw}" = "xyes"])

dnl for soundfile reading (and writing, if we do that...)
AC_ARG_WITH([sndfile], AC_HELP_STRING([--without-sndfile], [compile without libsndfile support]))
have_sndfile="no"
AS_IF([test "xno" != "x${with_sndfile}"],[
   AC_CHECK_LIB([sndfile], [sf_close])
   AS_IF([test "x$ac_cv_lib_sndfile_sf_close" != "xyes"],[
      AC_CHECK_LIB([sndfile-1],[sf_close])
      ac_cv_lib_sndfile_sf_close=$ac_cv_lib_sndfile_1_sf_close
   ])
   AS_IF([test "x$ac_cv_lib_sndfile_sf_close" = "xyes"],[
       AC_CHECK_HEADERS([sndfile.h], [have_sndfile="yes"])
   ])
])
AS_IF([test "xyes" = "x${have_sndfile}"],[
   AC_DEFINE([HAVE_LIBSNDFILE],1,[Define to 1 if you have the 'sndfile' library (-lsndfile).])
   AC_DEFINE([HAVE_SNDFILE_H],1,[Define to 1 if you have the <sndfile.h> header file.])
])
AM_CONDITIONAL(HAVE_SNDFILE, [test "xyes" = "x${have_sndfile}"])


dnl for gnu scientific library -lgsl:
AC_ARG_WITH([gsl], AC_HELP_STRING([--without-gsl], [compile without GNU Scientific Library]))
AS_IF([test "xno" != "x${with_gsl}"],[
   AC_CHECK_LIB([gslcblas], [cblas_dgemm])
   AC_CHECK_LIB([gsl], [gsl_blas_dgemm])
   AS_IF([test "x${ac_cv_lib_gsl_gsl_blas_dgemm}" = "xyes"],[
        AC_CHECK_LIB([gsl], [gsl_eigen_nonsymm], [:])
        AC_CHECK_LIB([gsl], [gsl_sf_bessel_Jn], [:])
   ])
])
AM_CONDITIONAL(HAVE_GSL, [test "x${ac_cv_lib_gsl_gsl_blas_dgemm}" = "xyes"])
AM_CONDITIONAL(HAVE_GSL_CBLAS, [test "x${ac_cv_lib_gslcblas_cblas_dgemm}" = "xyes"])
AS_IF([test "x${ac_cv_lib_gsl_gsl_blas_dgemm}" = "xyes"],[
   AC_DEFINE(HAVE_LIBGSL,1,[Define to 1 if you have the 'gsl' library (-lgsl).])
])
AS_IF([test "x${ac_cv_lib_gslcblas_cblas_dgemm}" = "xyes"],[
   AC_DEFINE(HAVE_LIBGSLCBLAS,1,[Define to 1 if you have the 'gslcblas' library (-lgslcblas).])
])
AS_IF([test "x${ac_cv_lib_gsl_gsl_eigen_nonsymm}" = "xyes"],[
   AC_DEFINE(HAVE_GSL_EIGEN_NONSYMM,1,[can gsl compute complex eigenvalues?])
])
AM_CONDITIONAL(HAVE_GSL_EIGEN, [test "x${ac_cv_lib_gsl_gsl_eigen_nonsymm}" = "xyes"])

AS_IF([test "x${ac_cv_lib_gsl_gsl_sf_bessel_Jn}" = "xyes"],[
   AC_DEFINE(HAVE_GSL_BESSEL,1,[can gsl compute Bessel functions?])
])
AM_CONDITIONAL(HAVE_GSL_BESSEL, [test "x${ac_cv_lib_gsl_sf_bessel_Jn}" = "xyes"])

AC_MSG_CHECKING([build-date])
AS_IF([test "x$with_build_date" = "xyes" ],[with_build_date=""])
AS_IF([test "x$with_build_date" = "xno"  ],[with_build_date=""])
AS_IF([test "x$with_build_date" != "x"  ],[ AC_DEFINE_UNQUOTED([BUILD_DATE], ["$with_build_date"], [user-defined build-date string])])
## urgh, brackets need to be escaped with @<:@ and @:>@...
AS_IF([test "x$with_build_date" != "x"  ],[ with_build_date="@<:@default@:>@" ])
AC_MSG_RESULT([$with_build_date])

AC_SUBST([CPPFLAGS])
AC_SUBST([CFLAGS])
AC_SUBST([LIBS])
AC_SUBST([DEFS])
AC_SUBST([ARCH_FLAG])
AC_SUBST([LIBTOOL_DEPS])
AC_SUBST([EXTRA_LTFLAGS])
AC_SUBST(EXTENSION)

AC_OUTPUT()

