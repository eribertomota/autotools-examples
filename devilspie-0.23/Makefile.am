SUBDIRS = po src tests

ACLOCAL_AMFLAGS = ${ACLOCAL_FLAGS}

man_MANS = devilspie.1

EXTRA_DIST = \
	devilspie.spec.in devilspie.spec \
	$(man_MANS)

INTLTOOL_BUILT = \
	intltool-extract \
	intltool-merge \
	intltool-update
DISTCLEANFILES = $(INTLTOOL_BUILT)
