# Automake makefile for lbcd.
#
# Written by Russ Allbery <eagle@eyrie.org>
# Copyright 1996, 1997, 1998, 2003, 2004, 2005, 2006, 2008, 2009, 2012, 2013
#     The Board of Trustees of the Leland Stanford Junior University
#
# See LICENSE for licensing terms.

ACLOCAL_AMFLAGS = -I m4
EXTRA_DIST = .gitignore LICENSE autogen server/arch/aix.c server/arch/bsd.c \
	server/arch/darwin.c server/arch/hpux10.c server/arch/hpux9.c	    \
	server/arch/irix.c server/arch/linux.c server/arch/osf.c	    \
	server/arch/solaris.c server/lbcd.8.in server/lbcd.pod		    \
	systemd/lbcd.service.in systemd/lbcd.socket tests/README	    \
	tests/TESTS tests/data/perl.conf tests/data/perlcriticrc	    \
	tests/data/perltidyrc tests/docs/pod-spelling-t tests/docs/pod-t    \
	tests/perl/critic-t tests/perl/minimum-version-t		    \
	tests/perl/strict-t tests/tap/libtap.sh tests/tap/perl/Test/RRA.pm  \
	tests/tap/perl/Test/RRA/Automake.pm				    \
	tests/tap/perl/Test/RRA/Config.pm tests/util/xmalloc-t

# Override systemdsystemunitdir when running distcheck so that we don't try
# to install files in the system directory.
DISTCHECK_CONFIGURE_FLAGS = \
	--with-systemdsystemunitdir=$$dc_install_base/$(systemdsystemunitdir)

# Supporting convenience libraries used by other targets.
noinst_LIBRARIES = modules/libmodules.a portable/libportable.a util/libutil.a
portable_libportable_a_SOURCES = portable/dummy.c portable/getaddrinfo.h \
	portable/getnameinfo.h portable/macros.h portable/sd-daemon.h	 \
	portable/socket.h portable/statvfs.h portable/stdbool.h		 \
	portable/system.h portable/uio.h
portable_libportable_a_LIBADD = $(LIBOBJS)
modules_libmodules_a_SOURCES = modules/check_reply.c modules/ftp.c	 \
	modules/http.c modules/imap.c modules/ldap.c modules/modules.h	 \
	modules/monlist.c modules/monlist.h modules/nntp.c modules/ntp.c \
	modules/pop.c modules/smtp.c modules/tcp.c modules/tcp_socket.c	 \
	modules/udp_socket.c
util_libutil_a_SOURCES = util/fdflag.c util/fdflag.h util/macros.h	\
	util/messages.c util/messages.h util/network.c util/network.h	\
	util/vector.c util/vector.h util/xmalloc.c util/xmalloc.h	\
	util/xwrite.c util/xwrite.h

# The lbcd listener daemon.
sbin_PROGRAMS = server/lbcd
server_lbcd_SOURCES = server/get_user.c server/kernel.c server/internal.h \
	server/lbcd.c server/load.c server/protocol.h server/server.c	  \
	server/tmp_full.c server/weight.c
server_lbcd_CPPFLAGS = -DLBCD_SENTINEL_FILE='"$(sysconfdir)/nolbcd"' \
	$(SYSTEMD_CFLAGS)
server_lbcd_LDADD = modules/libmodules.a util/libutil.a \
	portable/libportable.a $(SYSTEMD_LIBS)
man_MANS = server/lbcd.8

# The lbcdclient command-line query tool.
dist_bin_SCRIPTS = client/lbcdclient
dist_man_MANS = client/lbcdclient.1

# Substitute the installation paths into the systemd unit file.
systemd/lbcd.service: $(srcdir)/systemd/lbcd.service.in
	mkdir -p systemd
	sed -e 's![@]sbindir[@]!$(sbindir)!g' \
	    $(srcdir)/systemd/lbcd.service.in > $@

# Install the systemd unit file if systemd support was detected.
if HAVE_SYSTEMD
systemdsystemunit_DATA = systemd/lbcd.service systemd/lbcd.socket
endif

# Substitute the system configuration path into the manual page.
server/lbcd.8: $(srcdir)/server/lbcd.8.in
	sed 's%\(\\f(CI\)*\@sysconfdir\(\\fI\)*\@%$(sysconfdir)%' \
	    < $(srcdir)/server/lbcd.8.in > $@

# Clean rules.  Work around a misfeature of Automake and remove all the
# results of running autogen.
CLEANFILES = server/lbcd.8 systemd/lbcd.service
MAINTAINERCLEANFILES = Makefile.in aclocal.m4 build-aux/compile		\
	build-aux/config.guess build-aux/config.sub build-aux/depcomp	\
	build-aux/install-sh build-aux/missing config.h.in config.h.in~	\
	configure server/lbcd.8.in client/lbcdclient.1

# A set of flags for warnings.  Add -O because gcc won't find some warnings
# without optimization turned on.  Desirable warnings that can't be turned
# on due to other problems:
#
#     -Wconversion	http://bugs.debian.org/488884 (htons warnings)
#
# Last checked against gcc 4.8.2 (2014-04-12).  -D_FORTIFY_SOURCE=2 enables
# warn_unused_result attribute markings on glibc functions on Linux, which
# catches a few more issues.
if WARNINGS_GCC
    WARNINGS = -g -O -fstrict-overflow -fstrict-aliasing -D_FORTIFY_SOURCE=2 \
	-Wall -Wextra -Wendif-labels -Wformat=2 -Winit-self -Wswitch-enum    \
	-Wstrict-overflow=5 -Wfloat-equal -Wdeclaration-after-statement	     \
	-Wshadow -Wpointer-arith -Wbad-function-cast -Wcast-align	     \
	-Wwrite-strings -Wjump-misses-init -Wlogical-op -Wstrict-prototypes  \
	-Wold-style-definition -Wmissing-prototypes -Wnormalized=nfc	     \
	-Wpacked -Wredundant-decls -Wnested-externs -Winline -Wvla -Werror
endif
if WARNINGS_CLANG
    WARINGS = -Weverything -Wno-padded
endif

warnings:
	$(MAKE) V=0 CFLAGS='$(WARNINGS)'
	$(MAKE) V=0 CFLAGS='$(WARNINGS)' $(check_PROGRAMS)

# The bits below are for the test suite, not for the main package.
check_PROGRAMS = tests/runtests tests/portable/asprintf-t		   \
	tests/portable/daemon-t tests/portable/getaddrinfo-t		   \
	tests/portable/getnameinfo-t tests/portable/inet_aton-t		   \
	tests/portable/inet_ntoa-t tests/portable/inet_ntop-t		   \
	tests/portable/snprintf-t tests/portable/strlcat-t		   \
	tests/portable/strlcpy-t tests/portable/strndup-t		   \
	tests/server/basic-t tests/server/errors-t tests/util/fdflag-t	   \
	tests/util/messages-t tests/util/network/addr-ipv4-t		   \
	tests/util/network/addr-ipv6-t tests/util/network/client-t	   \
	tests/util/network/server-t tests/util/vector-t tests/util/xmalloc \
	tests/util/xwrite-t
tests_runtests_CPPFLAGS = -DSOURCE='"$(abs_top_srcdir)/tests"' \
        -DBUILD='"$(abs_top_builddir)/tests"'
check_LIBRARIES = tests/tap/libtap.a
tests_tap_libtap_a_SOURCES = tests/tap/basic.c tests/tap/basic.h	\
	tests/tap/lbcd.c tests/tap/lbcd.h tests/tap/macros.h		\
	tests/tap/process.c tests/tap/process.h tests/tap/string.c	\
	tests/tap/string.h

# All of the test programs.
tests_portable_asprintf_t_SOURCES = tests/portable/asprintf-t.c \
	tests/portable/asprintf.c
tests_portable_asprintf_t_LDADD = tests/tap/libtap.a portable/libportable.a
tests_portable_daemon_t_SOURCES = tests/portable/daemon-t.c \
	tests/portable/daemon.c
tests_portable_daemon_t_LDADD = tests/tap/libtap.a portable/libportable.a
tests_portable_getaddrinfo_t_SOURCES = tests/portable/getaddrinfo-t.c \
	tests/portable/getaddrinfo.c
tests_portable_getaddrinfo_t_LDADD = tests/tap/libtap.a portable/libportable.a
tests_portable_getnameinfo_t_SOURCES = tests/portable/getnameinfo-t.c \
	tests/portable/getnameinfo.c
tests_portable_getnameinfo_t_LDADD = tests/tap/libtap.a util/libutil.a \
	portable/libportable.a
tests_portable_inet_aton_t_SOURCES = tests/portable/inet_aton-t.c \
	tests/portable/inet_aton.c
tests_portable_inet_aton_t_LDADD = tests/tap/libtap.a portable/libportable.a
tests_portable_inet_ntoa_t_SOURCES = tests/portable/inet_ntoa-t.c \
	tests/portable/inet_ntoa.c
tests_portable_inet_ntoa_t_LDADD = tests/tap/libtap.a portable/libportable.a
tests_portable_inet_ntop_t_SOURCES = tests/portable/inet_ntop-t.c \
	tests/portable/inet_ntop.c
tests_portable_inet_ntop_t_LDADD = tests/tap/libtap.a portable/libportable.a
tests_portable_snprintf_t_SOURCES = tests/portable/snprintf-t.c \
	tests/portable/snprintf.c
tests_portable_snprintf_t_LDADD = tests/tap/libtap.a portable/libportable.a
tests_portable_strlcat_t_SOURCES = tests/portable/strlcat-t.c \
	tests/portable/strlcat.c
tests_portable_strlcat_t_LDADD = tests/tap/libtap.a portable/libportable.a
tests_portable_strlcpy_t_SOURCES = tests/portable/strlcpy-t.c \
	tests/portable/strlcpy.c
tests_portable_strlcpy_t_LDADD = tests/tap/libtap.a portable/libportable.a
tests_portable_strndup_t_SOURCES = tests/portable/strndup-t.c \
	tests/portable/strndup.c
tests_portable_strndup_t_LDADD = tests/tap/libtap.a portable/libportable.a
tests_server_basic_t_LDADD = tests/tap/libtap.a util/libutil.a \
	portable/libportable.a
tests_server_errors_t_LDADD = tests/tap/libtap.a util/libutil.a \
	portable/libportable.a
tests_util_fdflag_t_LDADD = tests/tap/libtap.a util/libutil.a \
	portable/libportable.a
tests_util_messages_t_LDADD = tests/tap/libtap.a util/libutil.a \
	portable/libportable.a
tests_util_network_addr_ipv4_t_LDADD = tests/tap/libtap.a util/libutil.a \
        portable/libportable.a
tests_util_network_addr_ipv6_t_LDADD = tests/tap/libtap.a util/libutil.a \
        portable/libportable.a
tests_util_network_client_t_LDADD = tests/tap/libtap.a util/libutil.a \
        portable/libportable.a
tests_util_network_server_t_LDADD = tests/tap/libtap.a util/libutil.a \
        portable/libportable.a
tests_util_vector_t_LDADD = tests/tap/libtap.a util/libutil.a \
	portable/libportable.a
tests_util_xmalloc_LDADD = util/libutil.a portable/libportable.a
tests_util_xwrite_t_SOURCES = tests/util/fakewrite.c tests/util/xwrite.c \
	tests/util/xwrite-t.c
tests_util_xwrite_t_LDADD = tests/tap/libtap.a util/libutil.a \
	portable/libportable.a

check-local: $(check_PROGRAMS)
	cd tests && ./runtests -l $(abs_top_srcdir)/tests/TESTS

# Used by maintainers to run the main test suite under valgrind.  Suppress
# the xmalloc and pod-spelling tests because the former won't work properly
# under valgrind (due to increased memory usage) and the latter is pointless
# to run under valgrind.
check-valgrind: $(check_PROGRAMS)
	rm -rf $(abs_top_builddir)/tmp-valgrind
	mkdir $(abs_top_builddir)/tmp-valgrind
	env RRA_MAINTAINER_TESTS= valgrind --leak-check=full	\
	    --show-reachable=yes --trace-children=yes		\
	    --log-file=$(abs_top_builddir)/tmp-valgrind/log.%p	\
	    --trace-children-skip="/bin/sh,*/cat,*/diff,*/expr,*/grep,*/mkdir,*/rm,*/rmdir,*/sed,*/sleep,*/true,*/wc,*/docs/*-t,*/perl/*-t" \
	    tests/runtests -l '$(abs_top_srcdir)/tests/TESTS'
