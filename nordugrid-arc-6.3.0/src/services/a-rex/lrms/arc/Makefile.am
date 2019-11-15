pkgpythondir = $(PYTHON_SITE_ARCH)/arc
pkgpython_PYTHON = __init__.py

all-local:
	if test ! -e "$(abs_top_builddir)/python/python/arc/lrms"; then ln -s $(abs_top_srcdir)/src/services/a-rex/lrms/arc/lrms $(abs_top_builddir)/python/python/arc/lrms; fi

CLEANFILES = $(abs_top_builddir)/python/python/arc/lrms

SUBDIRS = lrms
DIST_SUBDIRS = $(SUBDIRS)
