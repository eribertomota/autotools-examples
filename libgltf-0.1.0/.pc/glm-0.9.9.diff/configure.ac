# Process this file with autoconf to create configure.

AC_PREREQ([2.65])

# ====================
# Version informations
# ====================
m4_define([libgltf_version_major],[0])
m4_define([libgltf_version_minor],[1])
m4_define([libgltf_version_micro],[0])
m4_define([libgltf_version],[libgltf_version_major.libgltf_version_minor.libgltf_version_micro])

# =============
# Automake init
# =============
AC_INIT([libgltf],[libgltf_version])
AC_CONFIG_MACRO_DIR([m4])
AC_CONFIG_HEADERS([config.h])
AM_INIT_AUTOMAKE([1.11 foreign dist-xz dist-bzip2])
AM_SILENT_RULES([yes])
AC_LANG([C++])

# ===========================
# Find required base packages
# ===========================
AC_PROG_CXX
AC_PROG_CXXCPP
AC_PROG_INSTALL
AC_PROG_LN_S
AC_PROG_MAKE_SET
LT_INIT([pic-only])
PKG_PROG_PKG_CONFIG([0.20])

# =========
# Find boost
# =========
save_CPPFLAGS=$CPPFLAGS
CPPFLAGS="$CPPFLAGS $BOOST_CFLAGS"
AC_CHECK_HEADERS(
 boost/property_tree/ptree.hpp \
 boost/property_tree/json_parser.hpp \
 boost/foreach.hpp,
 [],
 [AC_MSG_ERROR(Required boost headers not found. Install boost >= 1.41.0)],
 [])
CPPFLAGS=$save_CPPFLAGS
AC_SUBST([BOOST_CFLAGS])

# =========
# Find epoxy
# =========
save_CPPFLAGS=$CPPFLAGS
CPPFLAGS="$CPPFLAGS $EPOXY_CFLAGS"
PKG_CHECK_MODULES(EPOXY, [epoxy >= 1.3.1], [] [
 AC_CHECK_HEADER(epoxy/gl.h, [],
 [AC_MSG_ERROR(epoxy/gl.h not found. install epoxy)], [])
])
CPPFLAGS=$save_CPPFLAGS
AC_SUBST([EPOXY_CFLAGS])
AC_SUBST([EPOXY_LIBS])

# =========
# Find glm
# =========
AC_LANG_PUSH([C++])
save_CPPFLAGS=$CPPFLAGS
CPPFLAGS="$CPPFLAGS $GLM_CFLAGS"
AC_CHECK_HEADERS(
 glm/glm.hpp \
 glm/gtc/matrix_inverse.hpp \
 glm/gtc/matrix_transform.hpp \
 glm/gtc/quaternion.hpp \
 glm/gtc/type_ptr.hpp \
 glm/gtx/quaternion.hpp \
 glm/gtx/rotate_vector.hpp \
 glm/gtx/transform.hpp,
 [],
 [AC_MSG_ERROR([Required glm headers not found. Install glm >= 0.9.0.0])],
 [])
AC_LANG_POP([C++])
CPPFLAGS=$save_CPPFLAGS
AC_SUBST([GLM_CFLAGS])

# =============================
# Check the needed time header
# =============================

AC_CHECK_HEADERS(
 sys/time.h,
 [],
 [AC_MSG_ERROR([Required sys/time.h not found.])],
 [])

AC_CHECK_FUNCS(
 gettimeofday,
 [],
 [AC_MSG_ERROR([Required gettimeofday() method is not found.])]
 )

# =================================
# Libtool/Version Makefile settings
# =================================
AC_SUBST(GLTF_MAJOR_VERSION, [libgltf_version_major])
AC_SUBST(GLTF_MINOR_VERSION, [libgltf_version_minor])
AC_SUBST(GLTF_MICRO_VERSION, [libgltf_version_micro])
AC_SUBST(GLTF_VERSION, [libgltf_version])
LT_CURRENT=`expr 100 '*' libgltf_version_major + libgltf_version_minor`
LT_AGE=0
AC_SUBST(LT_CURRENT)
AC_SUBST(LT_REVISION, [libgltf_version_micro])
AC_SUBST(LT_AGE)


# ================
# Check for cflags
# ================
AC_ARG_ENABLE([werror],
 [AS_HELP_STRING([--disable-werror], [Treat all warnings as errors, usefull for development])],
 [enable_werror="$enableval"],
 [enable_werror=yes]
)

AC_ARG_ENABLE([wparanoic],
 [AS_HELP_STRING([--enable-wparanoic], [Enable a lot of warnings...])],
 [enable_wparanoic="$enableval"],
 [enable_wparanoic=no]
)

AS_IF([test x"$enable_werror" != "xno"], [
 LIBGLTF_CXXFLAGS="$LIBGLTF_CXXFLAGS -Werror"
])
AS_IF([test x"$GCC" = xyes], [
# Be tough with warnings and produce less careless code
 LIBGLTF_CXXFLAGS="$LIBGLTF_CXXFLAGS -Wall -pedantic -Wextra -Weffc++ -Wshadow -Wendif-labels -Wundef -Wunused-macros"
])

AS_IF([test x"$enable_wparanoic" != "xno"], [
 LIBGLTF_CXXFLAGS="$LIBGLTF_CXXFLAGS -Wcast-align -Wcast-qual -Wchar-subscripts"
 LIBGLTF_CXXFLAGS="$LIBGLTF_CXXFLAGS -Wcomment -Wconversion -Wdisabled-optimization"
 LIBGLTF_CXXFLAGS="$LIBGLTF_CXXFLAGS -Wfloat-equal -Wformat -Wformat=2"
 LIBGLTF_CXXFLAGS="$LIBGLTF_CXXFLAGS -Wformat-nonliteral -Wformat-security"
 LIBGLTF_CXXFLAGS="$LIBGLTF_CXXFLAGS -Wformat-y2k -Wimport -Winit-self -Winvalid-pch"
 LIBGLTF_CXXFLAGS="$LIBGLTF_CXXFLAGS -Wmissing-braces -Wmissing-field-initializers"
 LIBGLTF_CXXFLAGS="$LIBGLTF_CXXFLAGS -Wmissing-format-attribute -Wmissing-include-dirs"
 LIBGLTF_CXXFLAGS="$LIBGLTF_CXXFLAGS -Wmissing-noreturn -Wpacked -Wparentheses"
 LIBGLTF_CXXFLAGS="$LIBGLTF_CXXFLAGS -Wpointer-arith -Wredundant-decls -Wreturn-type"
 LIBGLTF_CXXFLAGS="$LIBGLTF_CXXFLAGS -Wsequence-point -Wsign-compare -Wstrict-aliasing"
 LIBGLTF_CXXFLAGS="$LIBGLTF_CXXFLAGS -Wstrict-aliasing=2 -Wswitch -Wswitch-default"
 LIBGLTF_CXXFLAGS="$LIBGLTF_CXXFLAGS -Wswitch-enum -Wtrigraphs -Wunknown-pragmas -Wunused"
 LIBGLTF_CXXFLAGS="$LIBGLTF_CXXFLAGS -Wunused-function -Wunused-label -Wunused-parameter"
 LIBGLTF_CXXFLAGS="$LIBGLTF_CXXFLAGS -Wunused-value -Wvariadic-macros"
 LIBGLTF_CXXFLAGS="$LIBGLTF_CXXFLAGS -Wvolatile-register-var -Wwrite-strings"
])

AC_SUBST(LIBGLTF_CXXFLAGS)

# ============
# Debug switch
# ============
AC_ARG_ENABLE([debug],
 [AS_HELP_STRING([--enable-debug], [Turn on debugging])],
 [enable_debug="$enableval"],
 [enable_debug=no]
)
AS_IF([test "x$enable_debug" = "xyes"], [
 DEBUG_CXXFLAGS="-DDEBUG -g"
], [
 DEBUG_CXXFLAGS="-DNDEBUG"
])

AC_SUBST(DEBUG_CXXFLAGS)

# ==========
# Unit tests
# ==========
if test "$host_os" = "linux-gnu"; then

AC_ARG_ENABLE([tests],
 [AS_HELP_STRING([--enable-tests], [Build and run unit tests])],
 [enable_tests="$enableval"],
 [enable_tests=no]
)
AS_IF([test "x$enable_tests" = "xyes"], [
 PKG_CHECK_MODULES([CPPUNIT], [cppunit])
], [])
AC_SUBST([CPPUNIT_CFLAGS])
AC_SUBST([CPPUNIT_LIBS])

AS_IF([test "x$enable_tests" = "xyes"], [
 PKG_CHECK_MODULES([X11], [x11])
], [])
AC_SUBST([X11_CFLAGS])
AC_SUBST([X11_LIBS])

AS_IF([test "x$enable_tests" = "xyes"], [
 PKG_CHECK_MODULES([GL], [gl])
], [])
AC_SUBST([GL_CFLAGS])
AC_SUBST([GL_LIBS])

AS_IF([test "x$enable_tests" = "xyes"], [
 PKG_CHECK_MODULES([LIBPNG], [libpng])
], [])
AC_SUBST([LIBPNG_CFLAGS])
AC_SUBST([LIBPNG_LIBS])

AS_IF([test "x$enable_tests" = "xyes"], [
 AC_CHECK_HEADER(unistd.h, [], [AC_MSG_ERROR(unistd.h not found.)], [])
], [])

fi

AM_CONDITIONAL(TESTS, [test "x$enable_tests" = "xyes"])

# =====================
# Prepare all .in files
# =====================
AC_CONFIG_FILES([
Makefile
src/Makefile
inc/Makefile
build/Makefile
build/win32/Makefile
libgltf-$GLTF_MAJOR_VERSION.$GLTF_MINOR_VERSION.pc:libgltf.pc.in
qa/Makefile
qa/data/Makefile
qa/data/duck_model/Makefile
qa/data/duck_model/buffers/Makefile
qa/data/duck_model/shaders/Makefile
qa/data/duck_model/textures/Makefile
qa/helper/Makefile
qa/test/Makefile
])
AC_OUTPUT

# ==============================================
# Display final informations about configuration
# ==============================================
AC_MSG_NOTICE([
==============================================================================
Build configuration:
 debug: ${enable_debug}
 werror: ${enable_werror}
 tests: ${enable_tests}
==============================================================================
])


