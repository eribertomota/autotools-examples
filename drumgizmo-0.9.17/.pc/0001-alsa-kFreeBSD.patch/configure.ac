AC_INIT([drumgizmo], m4_esyscmd([cat version.h | cut -d'"' -f2 | xargs echo -n]))dnl"

AC_CONFIG_SRCDIR([src/drumgizmo.cc])
AM_INIT_AUTOMAKE

AC_PROG_CXX
AC_PROG_OBJC
AC_PROG_OBJCXX
AM_PROG_CC_C_O
AC_PROG_MKDIR_P

LT_INIT

AC_CONFIG_HEADERS(config.h)

AC_SYS_LARGEFILE

need_jack=no

dnl ===========================
dnl Compile with C++11 support.
dnl ===========================
AC_LANG_PUSH([C++])
TMP_CXXFLAGS="$CXXFLAGS"
CXXFLAGS=-std=c++11
AC_MSG_CHECKING([whether CXX supports -std=c++11])
AC_COMPILE_IFELSE([AC_LANG_PROGRAM([])],
	[AC_MSG_RESULT([yes])],
	[
	 AC_MSG_RESULT([no])
	 CXXFLAGS=-std=c++0x
	 AC_MSG_CHECKING([whether CXX supports -std=c++0x])
	 AC_COMPILE_IFELSE([AC_LANG_PROGRAM([])],
	 	[AC_MSG_RESULT([yes])],
	 	[
	 	 AC_MSG_RESULT([no])
	 	 AC_MSG_ERROR([Compiler does not support c++11])
	 	]
	 )
]
)
CXXFLAGS="$TMP_CXXFLAGS $CXXFLAGS"
OBJCXXFLAGS="$OBJCXXFLAGS $CXXFLAGS"
AC_LANG_POP([C++])

dnl ===========================
dnl Check for override /final keywords support
dnl ===========================
AC_LANG_PUSH([C++])
AC_MSG_CHECKING([whether 'override' and 'final' keywords are supported])
AC_COMPILE_IFELSE(
	[AC_LANG_SOURCE(
		[
			class A { virtual void foo() {} };
			class B : public A { virtual void foo() override {} };
			class C : public B { virtual void foo() final {} };
		]
	 )
	],
	[AC_MSG_RESULT([yes])],
	[AC_MSG_RESULT([no (deploying fix)])
	 CXXFLAGS="$CXXFLAGS -Doverride=\"\" -Dfinal=\"\""
	]
)
AC_LANG_POP([C++])

dnl ===========================
dnl Check for -ffloat-store support
dnl ===========================
AC_LANG_PUSH([C++])
TMP_CXXFLAGS="$CXXFLAGS"
CXXFLAGS="-Wall -Werror -ffloat-store"
AC_MSG_CHECKING([whether CXX supports -ffloat-store])
AC_COMPILE_IFELSE([AC_LANG_PROGRAM([])],
	[AC_MSG_RESULT([yes])
	 FLOAT_STORE="-ffloat-store"
	],
	[AC_MSG_RESULT([no])
	 FLOAT_STORE=""
	]
)
AC_SUBST(FLOAT_STORE)
CXXFLAGS="$TMP_CXXFLAGS"
AC_LANG_POP([C++])

dnl ======================
dnl Init pkg-config
dnl ======================
PKG_PROG_PKG_CONFIG(0.23)

HUGIN_PARM="-DDISABLE_HUGIN"
AC_ARG_WITH([debug],
	AS_HELP_STRING([--with-debug], [Build with debug support]))

dnl ===========================
dnl Check for -Wl,--no-undefined or -Wl,-undefined,error support
dnl ===========================
AC_LANG_PUSH([C++])
TMP_CXXFLAGS="$CXXFLAGS"
TMP_LDFLAGS="$LDFLAGS"
AC_MSG_CHECKING([whether linker supports '-Wl,-no-undefined'])
CXXFLAGS="-Wall -Werror"
LDFLAGS="-no-undefined"
AC_LINK_IFELSE([AC_LANG_PROGRAM([])],
	[ AC_MSG_RESULT([yes])
		NO_UNDEFINED_PARAM=-Wl,-no-undefined
	],
	[ AC_MSG_RESULT([no])
		AC_MSG_CHECKING([whether linker supports '-Wl,-undefined,error'])
		LDFLAGS="-undefined,error"
		AC_LINK_IFELSE([AC_LANG_PROGRAM([])],
			[AC_MSG_RESULT([yes])
				NO_UNDEFINED_PARAM=-Wl,-undefined,error
			],
			[AC_MSG_RESULT([no])
				NO_UNDEFINED_PARAM=""
			]
		)
	]
)
CXXFLAGS="$TMP_CXXFLAGS"
LDFLAGS="$TMP_LDFLAGS"
AC_LANG_POP([C++])

dnl ===========================
dnl Set up debug compile args if the user requested it
dnl ===========================
AS_IF([test "x$with_debug" == "xyes"],
      [AC_MSG_WARN([*** Building with debug support!])
	     CXXFLAGS="$CXXFLAGS -Wall -Werror -g $NO_UNDEFINED_PARAM"
	     HUGIN_PARM=""]
)

CXXFLAGS="$CXXFLAGS $HUGIN_PARM"

dnl ===========================
dnl Check for GUI backend
dnl ===========================
AC_CANONICAL_HOST
AC_ARG_ENABLE([gui],
	AS_HELP_STRING([--enable-gui[=backend]], [Use specified gui backend. Can be x11, win32, cocoa, pugl-x11, pugl-win32, pugl-cocoa or auto [default=auto]]),,
        [enable_gui="auto"])

AS_IF([test "x$enable_gui" = "xyes"], [enable_gui="auto"])

AS_IF([test "x$enable_gui" = "xauto"],
      [AC_MSG_RESULT([Auto setting gui based on host: $host_os])
	     AS_CASE([$host_os],
		      [darwin*], [enable_gui="cocoa"],
		      [linux*|*bsd*], [enable_gui="x11"],
		      [msys|mingw*|windows*|winnt|cygwin], [enable_gui="win32"],

		      AC_MSG_ERROR([Your platform is not currently supported])
	     )]
)

AS_IF(
  [test "x$enable_gui" = "xx11"],
  [AC_MSG_RESULT([Setting gui backend to X11])
  PKG_CHECK_MODULES(X11, x11 >= 1.0)
  PKG_CHECK_MODULES(XEXT, xext >= 1.0)
  GUI_CPPFLAGS="-DUI_X11 $X11_CFLAGS $XEXT_CFLAGS"
  GUI_LIBS="$X11_LIBS $XEXT_LIBS"],

  [test "x$enable_gui" = "xwin32"],
  [AC_MSG_RESULT([Setting gui backend to Win32])
  GUI_CPPFLAGS="-DUI_WIN32"
  GUI_LIBS="-lgdi32 -lsetupapi -lws2_32 -lcomctl32"],

  [test "x$enable_gui" = "xcocoa"],
  [AC_MSG_RESULT([Setting gui backend to Cocoa])
  GUI_CPPFLAGS="-DUI_COCOA"
  GUI_LIBS="-framework Cocoa"
	],

  [test "x$enable_gui" = "xpugl-x11"],
  [AC_MSG_RESULT([Setting gui backend to Pugl-X11])
  PKG_CHECK_MODULES(X11, x11 >= 1.0)
  PKG_CHECK_MODULES(XEXT, xext >= 1.0)
  GUI_CPPFLAGS="-DUI_PUGL -DPUGL_HAVE_GL $X11_CFLAGS $XEXT_CFLAGS"
  GUI_LIBS="-lGL $X11_LIBS $XEXT_LIBS"],

  [test "x$enable_gui" = "xpugl-win32"],
  [AC_MSG_RESULT([Setting gui backend to Pugl-Win32])
  GUI_CPPFLAGS="-DUI_PUGL -DPUGL_HAVE_GL"
  GUI_LIBS="-lopengl32 -lgdi32 -luser32 -lsetupapi -lws2_32 -lcomctl32"],

  [test "x$enable_gui" = "xpugl-cocoa"],
  [AC_MSG_RESULT([Setting gui backend to Pugl-Cocoa])
  GUI_CPPFLAGS="-DUI_PUGL -DPUGL_HAVE_GL"
  GUI_LIBS="-framework OpenGL -framework Cocoa"],

  AC_MSG_ERROR([*** No GUI backend has been selected ***])
)

AC_SUBST(GUI_CPPFLAGS)
AC_SUBST(GUI_LIBS)

AM_CONDITIONAL([ENABLE_X11], [test "x$enable_gui" = "xx11"])
AM_CONDITIONAL([ENABLE_WIN32], [test "x$enable_gui" = "xwin32"])
AM_CONDITIONAL([ENABLE_COCOA], [test "x$enable_gui" = "xcocoa"])
AM_CONDITIONAL([ENABLE_PUGL_X11], [test "x$enable_gui" = "xpugl-x11"])
AM_CONDITIONAL([ENABLE_PUGL_WIN32], [test "x$enable_gui" = "xpugl-win32"])
AM_CONDITIONAL([ENABLE_PUGL_COCOA], [test "x$enable_gui" = "xpugl-cocoa"])

dnl ===========================
dnl Custom number of outputs?
dnl ===========================
AC_ARG_ENABLE([custom-channel-count],
	AS_HELP_STRING([--enable-custom-channel-count[=count]], [Compile with specified number of output channels [default=16]]),,
        [enable_custom_channel_count="16"])
AC_DEFINE_UNQUOTED([NUM_CHANNELS], [$enable_custom_channel_count], [Number of output channels])

dnl ======================
dnl Compile unit tests
dnl ======================
AC_ARG_WITH([test],
	AS_HELP_STRING([--with-test], [Build unit tests]))

AM_CONDITIONAL([ENABLE_TESTS], [test "x$with_test" = "xyes"])

dnl ======================
dnl Compile LV2 plugin
dnl ======================
AC_ARG_ENABLE([lv2],
	AS_HELP_STRING([--enable-lv2], [Compile the LV2 plugin [default=no]]),,
        [enable_lv2="no"])

AS_IF(
  [test "x$enable_lv2" = "xyes"],
  [enable_lv2=yes
	 dnl ======================
	 dnl Check for lv2core
	 dnl ======================
	 PKG_CHECK_MODULES(LV2, lv2 >= 1.0)

	 dnl ======================
	 dnl Check for dl library
	 dnl ======================
	 tmp_CXXFLAGS="$CXXFLAGS"
	 tmp_CPPFLAGS="$CPPFLAGS"
	 tmp_CFLAGS="$CFLAGS"
	 tmp_LDFLAGS="$LDFLAGS"
	 tmp_LIBS="$LIBS"
	 CXXFLAGS=""
	 CPPFLAGS=""
	 CFLAGS=""
	 LDFLAGS=""
	 LIBS=""
	 AC_CHECK_HEADER(dlfcn.h, , AC_MSG_ERROR([*** dlfcn.h header file not found!]))
	 AC_CHECK_LIB(c,  dlopen, ,
		AC_CHECK_LIB(dl, dlopen, , AC_MSG_ERROR([*** library conaining dlopen not found!])))
	 DL_CFLAGS="$CXXFLAGS $CPPFLAGS $CFLAGS"
	 DL_LIBS="$LDFLAGS $LIBS"
	 CXXFLAGS="$tmp_CXXFLAGS"
	 CPPFLAGS="$tmp_CPPFLAGS"
	 CFLAGS="$tmp_CFLAGS"
	 LDFLAGS="$tmp_LDFLAGS"
	 LIBS="$tmp_LIBS"
	 AC_SUBST(DL_CFLAGS)
	 AC_SUBST(DL_LIBS)

	 AC_ARG_WITH([lv2dir],
		AS_HELP_STRING([--with-lv2dir=DIR],
		               [Use DIR as the lv2 plugin directory [default=LIBDIR/lv2]]),
	  [LV2DIR=$with_lv2dir],
	  [LV2DIR='$(libdir)/lv2'])
	 AC_SUBST(LV2DIR)
	],

  [AC_MSG_RESULT([*** LV2 plugin will not be compiled ***])
   enable_lv2=no]
)

AM_CONDITIONAL([ENABLE_LV2], [test "x$enable_lv2" = "xyes"])

dnl ======================
dnl Compile VST plugin
dnl ======================
AC_ARG_WITH([vst_sources],
	AS_HELP_STRING([--with-vst-sources], [Point this to the vstsdk24 directory]))
AC_ARG_ENABLE([vst],
	AS_HELP_STRING([--enable-vst], [Compile the VST plugin [default=no]]),,
        [enable_vst="no"])

AS_IF(
  [test "x$enable_vst" = "xyes"],
  [enable_vst=yes
  VST_CPPFLAGS="-D__int64='long long int'"

	# Set up platform specific workarounds for the VST SDK
	AS_CASE([$host_os],
		[darwin*], [ ],
		[linux*|*bsd*], [VST_CPPFLAGS="$VST_CPPFLAGS -D__cdecl="],
		[msys|mingw*|windows*|winnt|cygwin], [ ],
		AC_MSG_ERROR([Your platform is not currently supported])
	)

  VST_SOURCE_PATH="$with_vst_sources"
  AC_SUBST(VST_SOURCE_PATH)
  AC_SUBST(VST_CPPFLAGS)
  AC_CONFIG_FILES(plugin/Makefile.mingw32)],

  [AC_MSG_RESULT([*** VST plugin will not be compiled ***])
   enable_vst=no]
)

AM_CONDITIONAL([ENABLE_VST], [test "x$enable_vst" = "xyes"])


dnl ======================
dnl Compile AU plugin
dnl ======================
#AC_ARG_ENABLE([au],
#[  --enable-au   Compile the audio units plugin [default=no]],,
#        [enable_au="no"])
#if test "x$enable_au" = "xyes"; then
#	 enable_au=yes
#else
#	 AC_MSG_RESULT([*** Audio Units plugin will not be compiled ***])
#   enable_au=no
#fi
#AM_CONDITIONAL([ENABLE_AU], [test "x$enable_au" = "xyes"])

dnl ======================
dnl Compile cli client
dnl ======================
AC_ARG_ENABLE([cli],
	AS_HELP_STRING([--enable-cli], [Compile the command line interface [default=yes]]),,
        [enable_cli="yes"])


AS_IF(
  [test "x$enable_cli" = "xyes"],
  [enable_cli=yes

  dnl ======================
  dnl Check for getopt
  dnl ======================
  AC_CHECK_HEADERS(getopt.h)

  dnl ***
  dnl *** Input plugins
  dnl ***

  dnl *** Dummy
  AC_ARG_ENABLE([input_dummy],
		AS_HELP_STRING([--disable-input-dummy], [Disable input dummy plugin [default=enabled]]),,
           [enable_input_dummy="yes"])

  AS_IF(
    [test "x$enable_input_dummy" = "xyes"],
    [have_input_dummy=yes],

    [AC_MSG_RESULT([*** input dummy plugin disabled per user request ***])
     have_input_dummy=no]
  )

  dnl *** Test
  AC_ARG_ENABLE([input_test],
		AS_HELP_STRING([--disable-input-test], [Disable input test plugin [default=enabled]]),,
           [enable_input_test="yes"])

  AS_IF(
    [test "x$enable_input_test" = "xyes"],
    [have_input_test=yes],

    [AC_MSG_RESULT([*** input test plugin disabled per user request ***])
    have_input_test=no]
  )

  dnl *** Jackmidi
  AC_ARG_ENABLE([input_jackmidi],
    AS_HELP_STRING([--disable-input-jackmidi], [Disable input jackmidi plugin [default=enabled]]),,
           [enable_input_jackmidi="yes"])

  AS_IF(
    [test "x$enable_input_jackmidi" = "xyes"],
    [have_input_jackmidi=yes
    need_jack=yes],

    [AC_MSG_RESULT([*** input jackmidi plugin disabled per user request ***])
    have_input_jackmidi=no]
  )

  dnl *** Midifile
  AC_ARG_ENABLE([input_midifile],
		AS_HELP_STRING([--disable-input-midifile], [Disable input midifile plugin [default=enabled]]),,
           [enable_input_midifile="yes"])

  AS_IF(
    [test "x$enable_input_midifile" = "xyes"],
    [have_input_midifile=yes
		 dnl ======================
		 dnl Check for libsmf
		 dnl ======================
		 PKG_CHECK_MODULES(SMF, smf >= 1.2)],

    [AC_MSG_RESULT([*** input midifile plugin disabled per user request ***])
     have_input_midifile=no]
  )

  dnl *** oss
  case $host_os in
    freebsd*)
      enable_oss_midi_value=yes
      ;;
    *)
      enable_oss_midi_value=no
      ;;
  esac
  AC_ARG_ENABLE([input_oss],
    AS_HELP_STRING(
      [--disable-input-oss],
      [Disable input oss plugin [enabled by default on FreeBSD, disabled otherwise]]),,
    [enable_input_ossmidi=$enable_oss_midi_value]
  )

  AS_IF(
    [test "x$enable_input_ossmidi" = "xyes"],
    [AC_MSG_CHECKING(for OSS in)
      AC_COMPILE_IFELSE(
        [AC_LANG_SOURCE([[
          #include <sys/soundcard.h>
          #ifndef AFMT_S32_NE
          # error no oss
          #endif
        ]])],
        [
          have_input_ossmidi=yes
          AC_MSG_RESULT(yes)
        ],
        [AC_MSG_FAILURE([no OSS headers found])]
    )],

    [AC_MSG_RESULT([*** input ossmidi plugin disabled per user request ***])
    have_input_ossmidi=no]
  )

  INPUT_PLUGINS="midifile jackmidi dummy test ossmidi"
  AC_SUBST(INPUT_PLUGINS)

  dnl ***
  dnl *** Output plugins
  dnl ***

  dnl *** dummy
  AC_ARG_ENABLE([output_dummy],
		AS_HELP_STRING([--disable-output-dummy], [Disable output dummy plugin [default=enabled]]),,
           [enable_output_dummy="yes"])

  AS_IF(
    [test "x$enable_output_dummy" = "xyes"],
    [have_output_dummy=yes],

    [AC_MSG_RESULT([*** output dummy plugin disabled per user request ***])
     have_output_dummy=no]
  )

  dnl *** Jackaudio
  AC_ARG_ENABLE([output_jackaudio],
		AS_HELP_STRING([--disable-output-jackaudio], [Disable output jack plugin [default=enabled]]),,
           [enable_output_jackaudio="yes"])

  AS_IF(
    [test "x$enable_output_jackaudio" = "xyes"],
    [have_output_jackaudio=yes
     need_jack=yes],

    [AC_MSG_RESULT([*** output jack plugin disabled per user request ***])
     have_output_jackaudio=no]
  )

  dnl *** alsa
  AC_ARG_ENABLE([output_alsa],
		AS_HELP_STRING([--disable-output-alsa], [Disable output alsa plugin [default=enabled]]),,
           [enable_output_alsa="yes"])

  AS_IF(
    [test "x$enable_output_alsa" = "xyes"],
    [have_output_alsa=yes
     dnl ======================
     dnl Check for alsa library
     dnl ======================
     PKG_CHECK_MODULES(ALSA, alsa >= 1.0.18)],

    [AC_MSG_RESULT([*** output alsa plugin disabled per user request ***])
     have_output_alsa=no]
  )

  dnl *** wavfile
  AC_ARG_ENABLE([output_wavfile],
		AS_HELP_STRING([--disable-output-wavfile], [Disable output wavfile plugin [default=enabled]]),,
           [enable_output_wavfile="yes"])

  AS_IF(
    [test "x$enable_output_wavfile" = "xyes"],
    [have_output_wavfile=yes],

    [AC_MSG_RESULT([*** output wavfile plugin disabled per user request ***])
     have_output_wavfile=no]
  )

  dnl *** oss
  case $host_os in
    freebsd*)
      enable_oss_value=yes
      ;;
    *)
      enable_oss_value=no
      ;;
  esac
  AC_ARG_ENABLE([output_oss],
    AS_HELP_STRING(
      [--disable-output-oss],
      [Disable output oss plugin [enabled by default on FreeBSD, disabled otherwise]]),,
    [enable_output_oss=$enable_oss_value]
  )

  AS_IF(
    [test "x$enable_output_oss" = "xyes"],
    [AC_MSG_CHECKING(for OSS out)
      AC_COMPILE_IFELSE(
        [AC_LANG_SOURCE([[
          #include <sys/soundcard.h>
          #ifndef AFMT_S32_NE
          # error no oss
          #endif
        ]])],
        [
          have_output_oss=yes
          AC_MSG_RESULT(yes)
        ],
        [AC_MSG_FAILURE([no OSS headers found])]
    )],

    [AC_MSG_RESULT([*** output oss plugin disabled per user request ***])
    have_output_oss=no]
  )

  OUTPUT_PLUGINS="dummy alsa wavfile jackaudio oss"
  AC_SUBST(OUTPUT_PLUGINS)

  dnl
  dnl Setup plugin paths
  dnl
  dgplugindir=${libdir}/drumgizmo
  AC_SUBST([dgplugindir])
  INPUT_PLUGIN_DIR=${dgplugindir}/input
  OUTPUT_PLUGIN_DIR=${dgplugindir}/output
  AC_SUBST([INPUT_PLUGIN_DIR])
  AC_SUBST([OUTPUT_PLUGIN_DIR])],

  [AC_MSG_RESULT([*** Command line interface disabled per user request ***])
   enable_cli=no]
)

AM_CONDITIONAL([ENABLE_CLI], [test "x$enable_cli" == "xyes"])
AM_CONDITIONAL([HAVE_INPUT_DUMMY], [test "x$have_input_dummy" = "xyes"])
AM_CONDITIONAL([HAVE_INPUT_TEST], [test "x$have_input_test" = "xyes"])
AM_CONDITIONAL([HAVE_INPUT_JACKMIDI], [test "x$have_input_jackmidi" = "xyes"])
AM_CONDITIONAL([HAVE_INPUT_OSSMIDI], [test "x$have_input_ossmidi" = "xyes"])
AM_CONDITIONAL([HAVE_INPUT_MIDIFILE], [test "x$have_input_midifile" = "xyes"])
AM_CONDITIONAL([HAVE_OUTPUT_DUMMY], [test "x$have_output_dummy" = "xyes"])
AM_CONDITIONAL([HAVE_OUTPUT_ALSA], [test "x$have_output_alsa" = "xyes"])
AM_CONDITIONAL([HAVE_OUTPUT_WAVFILE], [test "x$have_output_wavfile" = "xyes"])
AM_CONDITIONAL([HAVE_OUTPUT_JACKAUDIO], [test "x$have_output_jackaudio" = "xyes"])
AM_CONDITIONAL([HAVE_OUTPUT_OSS], [test "x$have_output_oss" = "xyes"])

dnl ======================
dnl Check for sndfile
dnl ======================
PKG_CHECK_MODULES(SNDFILE, sndfile >= 1.0.20)


dnl ======================
dnl Check for the zitaresampler library
dnl ======================
AC_LANG_PUSH([C++])
tmp_CXXFLAGS="$CXXFLAGS"
tmp_CPPFLAGS="$CPPFLAGS"
tmp_CFLAGS="$CFLAGS"
tmp_LDFLAGS="$LDFLAGS"
tmp_LIBS="$LIBS"
CXXFLAGS=""
CPPFLAGS="$ZITA_CPPFLAGS"
CFLAGS=""
LDFLAGS="$ZITA_LDFLAGS"
LIBS="-lzita-resampler -lpthread"
AC_LINK_IFELSE(
  [AC_LANG_PROGRAM([#include <zita-resampler/resampler.h>],
    [Resampler r] ) ], has_zita=yes, has_zita=no)
ZITA_CPPFLAGS="$CXXFLAGS $CPPFLAGS $CFLAGS"
ZITA_LIBS="$LDFLAGS $LIBS"
CXXFLAGS="$tmp_CXXFLAGS"
CPPFLAGS="$tmp_CPPFLAGS"
CFLAGS="$tmp_CFLAGS"
LDFLAGS="$tmp_LDFLAGS"
LIBS="$tmp_LIBS"
AC_SUBST(ZITA_CPPFLAGS)
AC_SUBST(ZITA_LIBS)
AC_LANG_POP([C++])

dnl ======================
dnl Check for the rt library
dnl ======================
AC_HAVE_LIBRARY([rt],[],[])

dnl ======================
dnl Check for the atomic library
dnl ======================
AC_HAVE_LIBRARY([atomic],[],[])

dnl ======================
dnl Check for the pthread library
dnl ======================
tmp_CXXFLAGS="$CXXFLAGS"
tmp_CPPFLAGS="$CPPFLAGS"
tmp_CFLAGS="$CFLAGS"
tmp_LDFLAGS="$LDFLAGS"
tmp_LIBS="$LIBS"
CXXFLAGS=""
CPPFLAGS=""
CFLAGS=""
LDFLAGS=""
LIBS=""
AC_CHECK_HEADER(pthread.h, , AC_MSG_ERROR([*** pthread header file not found!]))
AC_CHECK_LIB(pthread,  pthread_mutex_init, , AC_MSG_ERROR([*** pthread library not found!]))
PTHREAD_CFLAGS="$CXXFLAGS $CPPFLAGS $CFLAGS"
PTHREAD_LIBS="$LDFLAGS $LIBS"
CXXFLAGS="$tmp_CXXFLAGS"
CPPFLAGS="$tmp_CPPFLAGS"
CFLAGS="$tmp_CFLAGS"
LDFLAGS="$tmp_LDFLAGS"
LIBS="$tmp_LIBS"
# Add extra (platform specific) libs for semaphore support?
AS_CASE([$host_os],
		      [darwin*], [PTHREAD_LIBS="$PTHREAD_LIBS -framework CoreServices"],
		      [linux*|*bsd*], [],
		      [msys|mingw*|windows*|winnt|cygwin], [],
					[])
AC_SUBST(PTHREAD_CFLAGS)
AC_SUBST(PTHREAD_LIBS)

dnl ===========================
dnl Check for SSE instructions
dnl ===========================
AC_ARG_ENABLE([sse],
	AS_HELP_STRING([--enable-sse[=level]], [Enable SSE Level 1, 2, 3 or auto [default=auto]]),,
        [enable_sse="auto"])

AS_IF([test "x$enable_sse" = "xyes"], [enable_sse="auto"])

#AC_MSG_RESULT([SSE: $enable_sse])

AS_IF([test "x$enable_sse" = "x3"],
      [AC_MSG_RESULT([Setting sse level 3])
       SSEFLAGS="-DSSE -msse -msse2 -mss3"],

      [test "x$enable_sse" = "x2"],
      [AC_MSG_RESULT([Setting sse level 2])
       SSEFLAGS="-DSSE -msse -msse2"],

      [test "x$enable_sse" = "x1"],
      [AC_MSG_RESULT([Setting sse level 1])
       SSEFLAGS="-DSSE -msse"],

      [test "x$enable_sse" = "xauto"],
      [AC_MSG_RESULT([Auto setting sse level])

       AC_MSG_CHECKING([for sse3 instructions])
       AS_IF([grep -q "sse3" /proc/cpuinfo],
             [AC_MSG_RESULT([yes])
              SSEFLAGS="-msse3"
              AC_SUBST(SSEFLAGS)],

             [AC_MSG_RESULT([no])]
       )

       AC_MSG_CHECKING([for sse2 instructions])
       AS_IF([grep -q "sse2" /proc/cpuinfo],
             [AC_MSG_RESULT([yes])
              SSEFLAGS="$SSEFLAGS -msse2"
              AC_SUBST(SSEFLAGS)],

             [AC_MSG_RESULT([no])]
       )

       AC_MSG_CHECKING([for sse instructions])
       AS_IF([grep -q "sse" /proc/cpuinfo],
             [AC_MSG_RESULT([yes])
              SSEFLAGS="$SSEFLAGS -DSSE -msse"
              AC_SUBST(SSEFLAGS)],

             [AC_MSG_RESULT([no])]
       )],

      [AC_MSG_RESULT([*** Disabling SSE ***])]
)

dnl ======================
dnl Check for jack
dnl ======================
AS_IF([test "x$need_jack" = "xyes"], [PKG_CHECK_MODULES(JACK, jack >= 0.120.1)])

AC_SUBST(CFLAGS)
AC_SUBST(CPPFLAGS)
AC_SUBST(CXXFLAGS)
AC_SUBST(LDFLAGS)
AC_SUBST(LIBS)

AC_CONFIG_FILES(
	Makefile
	tools/Makefile
	src/Makefile
	plugin/Makefile
	plugin/vst/Makefile
	plugingui/Makefile
	man/Makefile
	test/Makefile
	test/dgreftest/Makefile
	test/uitests/Makefile
	drumgizmo/Makefile)

AC_OUTPUT()
