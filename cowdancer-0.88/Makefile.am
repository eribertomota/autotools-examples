AUTOMAKE_OPTIONS = foreign
ACLOCAL_AMFLAGS = -I m4

SHELL = /bin/bash
bashcompletiondir = $(datadir)/bash-completion/completions

pkglib_LTLIBRARIES = libcowdancer.la
bin_PROGRAMS = cow-shell cowdancer-ilistcreate cowdancer-ilistdump
sbin_PROGRAMS = cowbuilder
man_MANS = cow-shell.1 cowdancer-ilistcreate.1 cowdancer-ilistdump.1 cowbuilder.8
bashcompletion_DATA = bash-completion/cowbuilder

FAST_TESTS = test_cowbuilder \
             test_cowbuilder_util \
             test_file \
             test_forkexec \
             test_ilistcreate \
             test_parameter

# Fragile; seen to fail on hurd-i386 with _FORTIFY_SOURCE=2, and Ubuntu ppc64el
# with -O3 (but not -O2, nor on Debian). Don't include it in the list for now.
# TODO: Investigate root cause.
# tests/016_memleakcheck.sh
SLOW_TESTS = tests/000_test_basic.sh \
             tests/001_test_symlink.sh \
             tests/002_test_open.sh \
             tests/003_test_fopen.sh \
             tests/004_test_fopen64.sh \
             tests/010_test_noilistfile.sh \
             tests/012_test_chown.sh \
             tests/013_test_chmod.sh \
             tests/014_ilistdump_test.sh \
             tests/015_test_ilistdelete.sh \
             tests/017_tempfilecheck.sh \
             tests/018_testcxx.sh \
             tests/019_test_filename_with_space.sh \
             tests/020_test_lchown.sh \
             tests/021_test_open.sh \
             tests/022_kernel_waitpid.sh \
             tests/102_test_cowbuilder_debbuildopts.sh

if QEMUBUILDER
QEMUBUILDER = yes
sbin_PROGRAMS += qemubuilder
man_MANS += qemubuilder.8
bashcompletion_DATA += bash-completion/qemubuilder
FAST_TESTS += test_qemuarch test_qemuipsanitize
SLOW_TESTS += tests/101_test_qemubuilder_dumpconfig.sh
else
QEMUBUILDER = no
endif

TESTS = $(FAST_TESTS) $(SLOW_TESTS)
check_PROGRAMS = $(FAST_TESTS) \
                 tests/002_test_open \
                 tests/003_test_fopen \
                 tests/004_test_fopen64 \
                 tests/012_test_chown \
                 tests/013_test_chmod \
                 tests/015_test_ilistdelete \
                 tests/016_memleakcheck \
                 tests/018_testcxx \
                 tests/021_test_open \
                 tests/022_kernel_waitpid

AM_CFLAGS = -fno-strict-aliasing -DCOWDANCER_SO="\"$(pkglibdir)/libcowdancer.so\""

libcowdancer_la_SOURCES = cowdancer.c ilistcreate.c log.c
## Effectively a no-op, but causes libcowdancer's object files to have a prefix
## so they don't clash with the non-libtool versions.
libcowdancer_la_CFLAGS = $(AM_CFLAGS)
## This is an internal library, so disable versioning, and don't build a static
## library
libcowdancer_la_LDFLAGS = -avoid-version -shared
cow_shell_SOURCES = cow-shell.c ilistcreate.c log.c
cowdancer_ilistcreate_SOURCES = cowdancer-ilistcreate.c ilistcreate.c log.c
cowdancer_ilistdump_SOURCES = cowdancer-ilistdump.c log.c
cowbuilder_SOURCES = cowbuilder.c parameter.c forkexec.c ilistcreate.c main.c cowbuilder_util.c log.c
qemubuilder_SOURCES = qemubuilder.c parameter.c forkexec.c qemuipsanitize.c qemuarch.c file.c main.c log.c
qemubuilder_CFLAGS = $(shell getconf LFS_CFLAGS) $(AM_CFLAGS)

test_cowbuilder_SOURCES = test_cowbuilder.c cowbuilder.c parameter.c forkexec.c ilistcreate.c cowbuilder_util.c log.c
test_cowbuilder_util_SOURCES = test_cowbuilder_util.c cowbuilder_util.c log.c
test_file_SOURCES = test_file.c file.c forkexec.c log.c
test_forkexec_SOURCES = test_forkexec.c forkexec.c log.c
test_ilistcreate_SOURCES = test_ilistcreate.c ilistcreate.c log.c
test_parameter_SOURCES = test_parameter.c parameter.c log.c
test_qemuarch_SOURCES = test_qemuarch.c qemuarch.c file.c log.c
test_qemuipsanitize_SOURCES = test_qemuipsanitize.c qemuipsanitize.c log.c

tests_004_test_fopen64_CPPFLAGS = $(AM_CPPFLAGS) -D_FILE_OFFSET_BITS=64
tests_015_test_ilistdelete_CPPFLAGS = $(AM_CPPFLAGS) -pthread
tests_015_test_ilistdelete_LDFLAGS = $(AM_LDFLAGS) -pthread
tests_016_memleakcheck_CFLAGS = $(AM_CFLAGS) -g
tests_018_testcxx_SOURCES = tests/018_testcxx.cc

AM_TESTS_ENVIRONMENT = COWDANCER_SO=$(abs_builddir)/@objdir@/libcowdancer.so; \
                       export COWDANCER_SO; \
                       PATH="$(abs_builddir):$(abs_builddir)/@objdir@:$(abs_srcdir)/tests:$$PATH"; \
                       export PATH;
