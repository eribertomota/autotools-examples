if PYTHON_SWIG_ENABLED
INITPY =
else
INITPY = __init__.py
endif

pkgpythondir = $(PYTHON_SITE_ARCH)/arc
pkgpython_PYTHON = paths.py $(INITPY)
nodist_pkgpython_PYTHON = paths_dist.py

paths_dist.py: gen_paths_dist.sh
	$(SHELL) $(builddir)/gen_paths_dist.sh > $@

CLEANFILES = paths_dist.py

SUBDIRS = utils control
DIST_SUBDIRS = utils control
