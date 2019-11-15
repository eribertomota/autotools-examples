
lib_LTLIBRARIES = libiconv_hook.la

libiconv_hook_la_SOURCES = \
	iconv_hook.c iconv_hook_default.c iconv_hook_eucjp.c \
	iconv_hook_ja_auto.c iconv_hook_mssjis.c iconv_hook_ucs2_cp932.c \
	iconv_hook_utf8_cp932.c iconv_hook_utf8_eucjp.c identify_encoding.c \
	cp.h iconv_hook.h identify_encoding.h ucs2_cp932.h
libiconv_hook_la_LIBADD  =
libiconv_hook_la_LDFLAGS = -version-info 1:0:0

includedir = @includedir@/iconv_hook

include_HEADERS = iconv_hook.h

EXTRA_DIST = iconv.h.replace

install-data-hook:
	$(INSTALL_DATA) iconv.h.replace $(DESTDIR)$(includedir)/iconv.h

uninstall-local:
	rm -f $(DESTDIR)$(includedir)/iconv.h
