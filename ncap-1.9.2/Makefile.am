AM_CFLAGS = @EXTRA_CFLAGS@

VERSION_INFO = 44:0:0

dist_man_MANS = ncap.3

include_HEADERS = ncap.h ncaptool.h ncap_list.h

lib_LTLIBRARIES = libncap.la
libncap_la_CFLAGS = $(AM_CFLAGS) \
	@libbind_cflags@ \
	@libpcap_cflags@
libncap_la_SOURCES = ncap_create.c ncap_dns.c ncap_icmp.c ipreasm.c \
	ncap.h ncap_port.h ncap_pvt.h ipreasm.h ncap_port_net.h ncap_list.h \
	asprintf.c asprintf.h
libncap_la_LDFLAGS = -version-info $(VERSION_INFO) \
	-export-symbols-regex "^ncap_.*" \
	@libbind_ldflags@ @libbind_libs@ \
	@libpcap_ldflags@ @libpcap_libs@

bin_PROGRAMS = ncaptool
ncaptool_CFLAGS = $(AM_CFLAGS) @libbind_cflags@
ncaptool_SOURCES = ncaptool.c ncaptool_mod.c dump_dns.c \
	ncap.h ncaptool.h ncaptool_mod.h ncap_port.h dump_dns.h
ncaptool_LDADD = libncap.la
ncaptool_LDFLAGS = @libbind_ldflags@ @libbind_libs@

wrapsrv_CFLAGS = $(AM_CFLAGS) @libbind_cflags@
wrapsrv_SOURCES = wrapsrv.c
wrapsrv_LDFLAGS = @libbind_ldflags@ @libbind_libs@

moduledir = $(libdir)/ncaptool
module_LTLIBRARIES = mod_test.la

mod_test_la_LDFLAGS = -module -avoid-version
mod_test_la_SOURCES = mod_test.c

EXTRA_DIST = \
	FILTERS \
	ncaptool-dnsparse.pl \
	pyncap/README \
	pyncap/ncap.c \
	pyncap/ncap.pyx \
	pyncap/setup.py \
	pyncap/test.py \
	pyncap/wrap.c \
	pyncap/wrap.h
