# Automake makefile for pam-afs-session.
#
# Written by Russ Allbery <eagle@eyrie.org>
# Copyright 2015 Russ Allbery <eagle@eyrie.org>
# Copyright 2006, 2007, 2010, 2011
#     The Board of Trustees of the Leland Stanford Junior University
#
# See LICENSE for licensing terms.

ACLOCAL_AMFLAGS = -I m4
EXTRA_DIST = .gitignore LICENSE autogen examples/debian/common-account	\
	examples/debian/common-auth examples/debian/common-session	\
	examples/redhat/system-auth examples/solaris/pam.conf		\
	pam_afs_session.map pam_afs_session.pod pam_afs_session.sym	\
	tests/README tests/TESTS tests/data/krb5-pam.conf		\
	tests/data/fake-aklog tests/data/krb5.conf tests/data/perl.conf	\
	tests/data/scripts tests/docs/pod-spelling-t tests/docs/pod-t	\
	tests/fakepam/README tests/kafs/basic-t tests/module/full-t	\
	tests/tap/libtap.sh tests/tap/perl/Test/RRA.pm			\
	tests/tap/perl/Test/RRA/Automake.pm				\
	tests/tap/perl/Test/RRA/Config.pm

# The following library order matters for annoying reasons.  libafsauthent
# contains its own com_err implementation, which we do not want to pick up.
#
# If pam_afs_session calls com_err functions directly, configure adds
# -lcom_err to the link line explicitly.  In that case, we want to link with
# the AFS libraries last, after -lcom_err, so that we don't use its com_err
# implementation.  If pam_afs_session doesn't call com_err functions, we
# want to link with the AFS libraries first, since otherwise in the
# --enable-reduced-depends case the linker may try to resolve the com_err
# symbols in libkrb5 from the AFS libraries.
#
# This is thankfully all fixed in later versions of AFS, which rename all
# the com_err symbols so that they don't conflict.  But we still support
# older versions.
if KRB5_USES_COM_ERR
    DEPEND_LIBS = $(KRB5_LIBS) $(KAFS_LIBS)
else
    DEPEND_LIBS = $(KAFS_LIBS) $(KRB5_LIBS)
endif

AM_CPPFLAGS = $(KAFS_CPPFLAGS) $(KRB5_CPPFLAGS)

noinst_LTLIBRARIES = pam-util/libpamutil.la portable/libportable.la
portable_libportable_la_SOURCES = portable/dummy.c portable/krb5.h	\
	portable/macros.h portable/pam.h portable/stdbool.h		\
	portable/system.h
portable_libportable_la_LIBADD = $(LTLIBOBJS)
pam_util_libpamutil_la_SOURCES = pam-util/args.c pam-util/args.h	\
	pam-util/logging.c pam-util/logging.h pam-util/options.c	\
	pam-util/options.h pam-util/vector.c pam-util/vector.h
pam_util_libpamutil_la_LDFLAGS = $(KRB5_LDFLAGS)
pam_util_libpamutil_la_LIBADD = $(DEPEND_LIBS)

if NEED_KAFS
    noinst_LTLIBRARIES += kafs/libkafs.la
    EXTRA_kafs_libkafs_la_SOURCES = kafs/sys-darwin10.c kafs/sys-darwin8.c \
	kafs/sys-linux.c kafs/sys-solaris.c kafs/sys-syscall.c
    kafs_libkafs_la_SOURCES = kafs/kafs.c portable/kafs.h portable/macros.h \
	portable/stdbool.h portable/system.h
    kafs_libkafs_la_LDFLAGS = $(KAFS_LDFLAGS)
    LIBKAFS = kafs/libkafs.la
endif

if HAVE_LD_VERSION_SCRIPT
    VERSION_LDFLAGS = -Wl,--version-script=${srcdir}/pam_afs_session.map
else
    VERSION_LDFLAGS = -export-symbols ${srcdir}/pam_afs_session.sym
endif

pamdir = $(libdir)/security
pam_LTLIBRARIES = pam_afs_session.la
pam_afs_session_la_SOURCES = internal.h options.c public.c tokens.c
pam_afs_session_la_LDFLAGS = -module -shared -avoid-version \
	$(VERSION_LDFLAGS) $(KAFS_LDFLAGS) $(KRB5_LDFLAGS)
pam_afs_session_la_LIBADD = pam-util/libpamutil.la portable/libportable.la \
	$(LIBKAFS) $(DEPEND_LIBS)
dist_man_MANS = pam_afs_session.5

MAINTAINERCLEANFILES = Makefile.in aclocal.m4 build-aux/config.guess	\
	build-aux/config.sub build-aux/depcomp build-aux/install-sh	\
	build-aux/ltmain.sh build-aux/missing config.h.in config.h.in~	\
	configure m4/libtool.m4 m4/ltoptions.m4 m4/ltsugar.m4		\
	m4/ltversion.m4 m4/lt~obsolete.m4 pam_afs_session.5

# A set of flags for warnings.  Add -O because gcc won't find some warnings
# without optimization turned on.  Desirable warnings that can't be turned
# on due to other problems:
#
#     -Wconversion      http://bugs.debian.org/488884 (htons warnings)
#
# Last checked against gcc 4.8.2 (2014-04-12).  -D_FORTIFY_SOURCE=2 enables
# warn_unused_result attribute markings on glibc functions on Linux, which
# catches a few more issues.
if WARNINGS_GCC
    WARNINGS = -g -O -fstrict-overflow -fstrict-aliasing -D_FORTIFY_SOURCE=2 \
        -Wall -Wextra -Wendif-labels -Wformat=2 -Winit-self -Wswitch-enum    \
        -Wstrict-overflow=5 -Wfloat-equal -Wdeclaration-after-statement      \
        -Wshadow -Wpointer-arith -Wbad-function-cast -Wcast-align            \
        -Wwrite-strings -Wjump-misses-init -Wlogical-op -Wstrict-prototypes  \
        -Wold-style-definition -Wmissing-prototypes -Wnormalized=nfc         \
        -Wpacked -Wredundant-decls -Wnested-externs -Winline -Wvla -Werror
endif
if WARNINGS_CLANG
    WARINGS = -Weverything -Wno-padded
endif

warnings:
	$(MAKE) V=0 CFLAGS='$(WARNINGS)'
	$(MAKE) V=0 CFLAGS='$(WARNINGS)' $(check_PROGRAMS)

# The bits below are for the test suite, not for the main package.
check_PROGRAMS = tests/runtests tests/kafs/basic tests/kafs/haspag-t	\
	tests/module/basic-t tests/module/cells-t tests/module/full	\
	tests/module/hasafs-t tests/module/pag-t tests/module/sigchld-t	\
	tests/pam-util/args-t tests/pam-util/fakepam-t			\
	tests/pam-util/logging-t tests/pam-util/options-t		\
	tests/pam-util/vector-t tests/portable/asprintf-t		\
	tests/portable/snprintf-t tests/portable/strlcat-t		\
	tests/portable/strlcpy-t tests/portable/strndup-t
tests_runtests_CPPFLAGS = -DSOURCE='"$(abs_top_srcdir)/tests"' \
	-DBUILD='"$(abs_top_builddir)/tests"'
check_LIBRARIES = tests/fakepam/libfakepam.a tests/module/libfakekafs.a	\
	tests/tap/libtap.a
tests_fakepam_libfakepam_a_SOURCES = tests/fakepam/config.c		  \
	tests/fakepam/data.c tests/fakepam/general.c			  \
	tests/fakepam/internal.h tests/fakepam/logging.c		  \
	tests/fakepam/pam.h tests/fakepam/script.c tests/fakepam/script.h \
	tests/fakepam/stubs.c
tests_module_libfakekafs_a_SOURCES = tests/module/fakekafs.c
tests_tap_libtap_a_CPPFLAGS = -I$(abs_top_srcdir)/tests
tests_tap_libtap_a_SOURCES = tests/tap/basic.c tests/tap/basic.h	\
	tests/tap/macros.h tests/tap/string.c tests/tap/string.h

# All of the test programs.
tests_kafs_basic_LDFLAGS = $(KAFS_LDFLAGS)
tests_kafs_basic_LDADD = portable/libportable.la $(LIBKAFS) $(DEPEND_LIBS)
tests_kafs_haspag_t_LDFLAGS = $(KAFS_LDFLAGS)
tests_kafs_haspag_t_LDADD = tests/tap/libtap.a portable/libportable.la \
	$(LIBKAFS) $(DEPEND_LIBS)
tests_module_basic_t_LDFLAGS = $(KAFS_LDFLAGS) $(KRB5_LDFLAGS)
tests_module_basic_t_LDADD = options.lo public.lo tokens.lo		     \
	pam-util/libpamutil.la tests/fakepam/libfakepam.a tests/tap/libtap.a \
	portable/libportable.la $(LIBKAFS) $(DEPEND_LIBS)
tests_module_cells_t_LDFLAGS = $(KAFS_LDFLAGS) $(KRB5_LDFLAGS)
tests_module_cells_t_LDADD = options.lo public.lo tokens.lo		     \
	pam-util/libpamutil.la tests/fakepam/libfakepam.a tests/tap/libtap.a \
	portable/libportable.la $(LIBKAFS) $(DEPEND_LIBS)
tests_module_full_LDFLAGS = $(KAFS_LDFLAGS) $(KRB5_LDFLAGS)
tests_module_full_LDADD = options.lo public.lo tokens.lo	\
	pam-util/libpamutil.la tests/fakepam/libfakepam.a	\
	tests/tap/libtap.a portable/libportable.la $(LIBKAFS)	\
	$(DEPEND_LIBS)
tests_module_hasafs_t_LDFLAGS = $(KAFS_LDFLAGS) $(KRB5_LDFLAGS)
tests_module_hasafs_t_LDADD = options.lo public.lo tokens.lo	\
	tests/module/libfakekafs.a pam-util/libpamutil.la	\
	tests/fakepam/libfakepam.a tests/tap/libtap.a		\
	portable/libportable.la
tests_module_pag_t_LDFLAGS = $(KAFS_LDFLAGS) $(KRB5_LDFLAGS)
tests_module_pag_t_LDADD = options.lo public.lo tokens.lo	\
	tests/module/libfakekafs.a pam-util/libpamutil.la	\
	tests/fakepam/libfakepam.a tests/tap/libtap.a		\
	portable/libportable.la
tests_module_sigchld_t_LDFLAGS = $(KAFS_LDFLAGS) $(KRB5_LDFLAGS)
tests_module_sigchld_t_LDADD = options.lo public.lo tokens.lo	\
	pam-util/libpamutil.la tests/fakepam/libfakepam.a	\
	tests/tap/libtap.a portable/libportable.la $(LIBKAFS)	\
	$(DEPEND_LIBS)
tests_pam_util_args_t_LDFLAGS = $(KRB5_LDFLAGS)
tests_pam_util_args_t_LDADD = pam-util/libpamutil.la	\
	tests/fakepam/libfakepam.a tests/tap/libtap.a	\
	portable/libportable.la $(KRB5_LIBS)
tests_pam_util_fakepam_t_LDADD = tests/fakepam/libfakepam.a	\
	tests/tap/libtap.a portable/libportable.la
tests_pam_util_logging_t_LDFLAGS = $(KRB5_LDFLAGS)
tests_pam_util_logging_t_LDADD = pam-util/libpamutil.la	\
	tests/fakepam/libfakepam.a tests/tap/libtap.a	\
	portable/libportable.la $(KRB5_LIBS)
tests_pam_util_options_t_LDFLAGS = $(KRB5_LDFLAGS)
tests_pam_util_options_t_LDADD = pam-util/libpamutil.la	\
	tests/fakepam/libfakepam.a tests/tap/libtap.a	\
	portable/libportable.la $(KRB5_LIBS)
tests_pam_util_vector_t_LDADD = pam-util/libpamutil.la	\
	tests/fakepam/libfakepam.a tests/tap/libtap.a	\
	portable/libportable.la
tests_portable_asprintf_t_SOURCES = tests/portable/asprintf-t.c \
	tests/portable/asprintf.c
tests_portable_asprintf_t_LDADD = tests/tap/libtap.a portable/libportable.la
tests_portable_snprintf_t_SOURCES = tests/portable/snprintf-t.c \
	tests/portable/snprintf.c
tests_portable_snprintf_t_LDADD = tests/tap/libtap.a portable/libportable.la
tests_portable_strlcat_t_SOURCES = tests/portable/strlcat-t.c \
	tests/portable/strlcat.c
tests_portable_strlcat_t_LDADD = tests/tap/libtap.a portable/libportable.la
tests_portable_strlcpy_t_SOURCES = tests/portable/strlcpy-t.c \
	tests/portable/strlcpy.c
tests_portable_strlcpy_t_LDADD = tests/tap/libtap.a portable/libportable.la
tests_portable_strndup_t_SOURCES = tests/portable/strndup-t.c \
	tests/portable/strndup.c
tests_portable_strndup_t_LDADD = tests/tap/libtap.a portable/libportable.la

check-local: $(check_PROGRAMS)
	cd tests && ./runtests -l $(abs_top_srcdir)/tests/TESTS
