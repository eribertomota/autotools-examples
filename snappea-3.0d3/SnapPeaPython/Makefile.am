SUBDIRS = CuspedCensusData installation

# Find the python version that we need to build against.
PYVER=$(shell pyversions -r ../debian/control)

INCLUDES = -I../SnapPeaKernel/headers -I../SnapPeaKernel/unix_kit \
  -I/usr/include/$(PYVER)

pkglib_LTLIBRARIES = SnapPeaC.la

SnapPeaC_la_SOURCES = SnapPeaC.c
SnapPeaC_la_LDFLAGS = -no-undefined -module -avoid-version
SnapPeaC_la_LIBADD = $(top_srcdir)/SnapPeaKernel/libsnappea.la

bin_SCRIPTS = snappea snappea-console

pythondir = $(pkgdatadir)/SnapPeaPython

python_DATA = SnapPea.py SnapPeaGUI.py links.py

EXTRA_DIST = SnapPea.c makefile open
