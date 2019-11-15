# Copyright (C) 2013 Ben Asselstine
# 
# Copying and distribution of this file, with or without modification,
# are permitted in any medium without royalty provided the copyright
# notice and this notice are preserved.  This file is offered as-is,
# without any warranty.
AM_COLOR_TESTS=no
AM_TESTS_ENVIRONMENT=export licensing=${top_builddir}/src/licensing; \
		     export builddir=${builddir}; \
		     export HOME=${builddir}; \
		     export LU_COMMENT_EXTRACTOR_DIR=${top_builddir}/src; \
		     export LU_LANGFILE_DIR=${top_srcdir}/lang-files;

top_tests=0001
TESTS=${top_tests}
check_SCRIPTS=${top_tests}

EXTRA_DIST=${top_tests}
