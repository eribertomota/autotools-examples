# lib must be before src, otherwise, the ldbashconfig command at src/Makefile.am will fail
SUBDIRS = lib . src doc m4 tests

AUTOMAKE_OPTIONS = -Wno-portability

EXTRA_DIST = libbash.man

# installing man pages
man7_MANS = libbash.man


# Running ldbashconfig after installation only if DESTDIR is empty
install-data-hook:
	[[ "$(DESTDIR)" == "" ]] && $(sbindir)/ldbashconfig || :
	@[[ "$(DESTDIR)" != "" ]] &&	(echo "===============================================" && \
									echo "You've used DESTDIR - not running ldbashconfig!" && \
									echo "===============================================") || :
