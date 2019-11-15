
# # svn info
# # $Author: morongo $
# # $Date: 2009-01-11 17:17:03 +0100 (dom, 11 ene 2009) $
# # $HeadURL: https://jaula.svn.sourceforge.net/svnroot/jaula/tags/jaula-1.4.0/Makefile.am $
# # $Id: Makefile.am 45 2009-01-11 16:17:03Z morongo $
# # $Revision: 45 $

# # First level directories
SUBDIRS = @SUBDIRS@

# # base data directory
datarootdir = @datarootdir@

# # Suggested by libtool
ACLOCAL_AMFLAGS=-I m4

EXTRA_DIST = TODO.lst

# # Automatic recompilation of dependencies
LIBTOOL_DEPS = @LIBTOOL_DEPS@
libtool: $(LIBTOOL_DEPS)
	$(SHELL) ./config.status --recheck

# # Target to generate project documentation
docs:
	make -C doc

# # EOF $Id: Makefile.am 45 2009-01-11 16:17:03Z morongo $

