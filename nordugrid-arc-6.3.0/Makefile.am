# /opt/local is the location for macports on MacOS X

ACLOCAL_AMFLAGS = -I m4 `test -d /opt/local/share/aclocal && echo -I /opt/local/share/aclocal`

if SWIG_ENABLED
SWIG_SD = swig
endif

SUBDIRS = src include $(SWIG_SD) python $(POSUB) debian

DIST_SUBDIRS = src include swig python po debian

EXTRA_DIST = nordugrid-arc.spec autogen.sh LICENSE NOTICE
