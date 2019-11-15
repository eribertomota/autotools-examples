# Make coreutils man pages.				-*-Makefile-*-

# Copyright (C) 2002-2007 Free Software Foundation, Inc.

# This program is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.

# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.

# You should have received a copy of the GNU General Public License
# along with this program.  If not, see <http://www.gnu.org/licenses/>.

dist_man_MANS = dc3dd.1

man_aux = $(dist_man_MANS:.1=.x)

EXTRA_DIST = $(man_aux) $(NO_INSTALL_PROGS_DEFAULT:%=%.x) help2man
MAINTAINERCLEANFILES = $(dist_man_MANS)

# Depend on configure.ac to get version number changes.
common_dep = $(top_srcdir)/configure.ac

# Note that arch depends on uname.c
dc3dd.1:	$(common_dep)	$(srcdir)/dc3dd.x		../src/dc3dd.c

SUFFIXES = .x .1

# Ensure that help2man runs the ../src/ginstall binary as
# `install' when creating install.1.
# Similarly, ensure that it uses the ../src/[ binary to create test.1.
t = $*.td
mapped_name = `echo $*|sed 's/^install$$/ginstall/; s/^test$$/[/'`

# Note the use of $t/$*, rather than just `$*' as in other packages.
# That is necessary to avoid failures for programs that are also shell built-in
# functions like echo, false, printf, pwd.
.x.1:
	@case '$(PERL)' in					\
	  *"/missing "*)					\
	    echo 'WARNING: cannot update man page $@ since perl is missing' \
	      'or inadequate' 1>&2 \
	    ;;							\
	  *)							\
	    rm -f $@						\
	    && { echo "Updating man page $@";			\
	         rm -rf $t;					\
	         mkdir $t;					\
	         (cd $t && $(LN_S) ../../src/$(mapped_name) $*); \
	            $(PERL) -- $(srcdir)/help2man		\
	             --source='$(PACKAGE_STRING)'		\
	             --include=$(srcdir)/$*.x			\
	             --output=$t/$@ $t/$*;			\
	       }						\
	    && sed 's|$*\.td/||g' $t/$@ > $@			\
	    && chmod a-w $@					\
	    && rm -rf $t ;;					\
	esac

check-local: check-x-vs-1 check-programs-vs-x

# Sort in traditional ASCII order, regardless of the current locale;
# otherwise we may get into trouble with distinct strings that the
# current locale considers to be equal.
ASSORT = LC_ALL=C sort

# Ensure that for each .x file in this directory, there is a
# corresponding .1 file in the definition of $(dist_man_MANS) above.
# But since that expansion usually lacks programs like su and arch,
# add them here manually.
.PHONY: check-x-vs-1
check-x-vs-1:
	PATH=../src$(PATH_SEPARATOR)$$PATH; export PATH;		\
	t=ls-files.$$$$;						\
	(cd $(srcdir) && ls -1 *.x) | sed 's/\.x$$//' | $(ASSORT) > $$t;\
	(echo $(dist_man_MANS) $(NO_INSTALL_PROGS_DEFAULT)		\
	  | tr -s ' ' '\n' | sed 's/\.1$$//')				\
	  | $(ASSORT) -u | diff - $$t || { rm $$t; exit 1; };		\
	rm $$t

all_programs =								\
      (cd ../src && MAKEFLAGS= $(MAKE) -s all_programs.list)		\
       | grep -v '\['

.PHONY: check-programs-vs-x
check-programs-vs-x:
	status=0;					\
	for p in dummy `$(all_programs)`; do		\
	  test $$p = dummy && continue;			\
	  test $$p = ginstall && p=install || : ;	\
	  test -f $(srcdir)/$$p.x			\
	    || { echo missing $$p.x 1>&2; status=1; };	\
	done;						\
	exit $$status
