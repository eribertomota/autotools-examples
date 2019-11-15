AC_PREREQ([2.57])

AC_INIT(libbash, 0.9.11, libbash-common@lists.sourcefoge.net)

AC_CONFIG_SRCDIR([src/ldbash.in])

AM_INIT_AUTOMAKE([dist-bzip2])

AC_PREFIX_DEFAULT([/usr])

#
# Check for programs we need
##############################################################################
AC_PROG_LN_S
AC_CHECK_PROG([DOXYGEN], [doxygen], [doxygen])

#
# Misc
##############################################################################
# this is used my html and man pages documentation
DOCDATE=[`awk --re-interval '/[\t ]{1,}[0-9]{4}-[0-9]{2}-[0-9]{2}/ {print $1; exit}' ChangeLog`]
DOCDATE=[`date -d $DOCDATE "+%B %d, %G"`]
AC_SUBST([docdate],[$DOCDATE])

AC_ARG_ENABLE([doc],AC_HELP_STRING([--disable-docs],[Don't build and install documentation]),
							[DOCS=$enableval],
							[DOCS="yes"]
							)
AM_CONDITIONAL(MAKEDOCS, test "$DOCS" == "yes" )


#
# Output files
##############################################################################

# Makefiles
AC_CONFIG_FILES([	Makefile
					src/Makefile
					lib/Makefile
					doc/Makefile
					m4/Makefile
					tests/Makefile])


# Documentation files
[[ "$DOCS" == "yes" ]] && \
AC_CONFIG_FILES([	doc/Doxyfile
					doc/main_page.dox])

# man pages
AC_CONFIG_FILES([	libbash.man
					lib/colors.man
					lib/getopts.man
					lib/hashstash.man
					lib/locks.man
					lib/messages.man
					lib/urlcoding.man
					src/ldbash.man
					src/ldbashconfig.man])

# Scripts in src
AC_CONFIG_FILES([	src/ldbash
					src/ldbashconfig])

# Libraries in lib
AC_CONFIG_FILES([	lib/locks.sh])

# Misc files
AC_CONFIG_FILES([	libbash.spec])

AC_OUTPUT

# prints warning if doxygen was not found
if [[ "X$DOXYGEN" == "X" ]] ; then
	echo
	echo
	echo -e "\tWARNING: doxygen was not found in your path."
	echo -e "\t         html documentation will not be generated."
	echo
	echo
fi
