#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ(2.59)
AC_INIT([libguess], [1.2], [bugs+libguess@atheme.org])
AC_CONFIG_SRCDIR([src/libguess/guess.c])
AC_CONFIG_HEADER([src/libguess/autoconf.h])
AC_CONFIG_MACRO_DIR([m4])

AC_CANONICAL_HOST
AC_CANONICAL_TARGET

# Checks for programs.
AC_PROG_CC
AC_PROG_LN_S
AC_PROG_INSTALL
AC_PROG_MAKE_SET
AC_ISC_POSIX

test x"$GCC" = x"yes" && CFLAGS="$CFLAGS -pipe -Wall"

# XXX workaround
PACKAGE="libguess"
AC_SUBST(PACKAGE)

# Checks for libraries.
BUILDSYS_SHARED_LIB
LIBS="$LIBS $DYNAMIC_LD_LIBS"

# Checks for header files.
AC_HEADER_DIRENT
AC_HEADER_STDC
AC_CHECK_HEADERS([limits.h stdlib.h string.h unistd.h locale.h stdarg.h sys/types.h sys/stat.h errno.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST

# Checks for library functions.
AC_FUNC_CLOSEDIR_VOID
AC_CHECK_FUNCS([memset setlocale strcasecmp strchr strdup strerror strtol strtod])
AC_CHECK_FUNCS([printf sprintf snprintf vsnprintf gettimeofday strndup strlcpy strlcat])
AC_FUNC_STAT

# Check for optional features.
EXAMPLES_BUILD=""
AC_ARG_ENABLE(examples,
    [  --enable-examples        build and install example programs],
    [enable_examples=$enableval],
    [enable_examples="no"]
)

if test "x$enable_examples" = "xyes"; then
	EXAMPLES_BUILD="examples"
fi

AC_SUBST(EXAMPLES_BUILD)

BUILDSYS_TOUCH_DEPS

AC_CONFIG_FILES([buildsys.mk extra.mk libguess.pc])
AC_OUTPUT

cat << _EOF_

Configuration:
	No special features yet.

Now type "make" to build, and "make install" to install.
Thank you for using libguess.

_EOF_
