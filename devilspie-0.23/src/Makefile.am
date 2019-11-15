# The main binary
bin_PROGRAMS = devilspie

devilspie_SOURCES = \
	devilspie.h \
	devilspie.c \
	xutils.h \
	xutils.c \
	e-sexp.h \
	e-sexp.c \
	parser.h \
	parser.c \
	logical.h \
	logical.c \
	matchers.h \
	matchers.c \
	actions.h \
	actions.c

TESTS = sexp-test
check_PROGRAMS = sexp-test
sexp_test_SOURCES = \
	sexp-test.c \
	xutils.h \
	xutils.c \
	e-sexp.h \
	e-sexp.c \
	parser.h \
	parser.c \
	logical.h \
	logical.c \
	matchers.h \
	matchers.c \
	actions.h \
	actions.c

AM_CPPFLAGS = \
	$(WNCK_CFLAGS) \
	-DLOCALEDIR=\""$(datadir)/locale"\" \
	-DSYSCONFDIR=\""$(sysconfdir)"\" \
	-DDATADIR=\""$(datadir)"\" \
	-DG_DISABLE_DEPRECATED \
	-DGDK_DISABLE_DEPRECATED \
	-DGTK_DISABLE_DEPRECATED \
	-DWNCK_I_KNOW_THIS_IS_UNSTABLE

AM_CFLAGS = @WARN_CFLAGS@

LDADD = ${WNCK_LIBS}
