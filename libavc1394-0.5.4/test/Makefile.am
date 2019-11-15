MAINTAINERCLEANFILES = Makefile.in
bin_PROGRAMS = dvcont mkrfc2734 panelctl
noinst_PROGRAMS = romtest setrom avc_vcr 
man_MANS = dvcont.1 mkrfc2734.1 panelctl.1
EXTRA_DIST = $(man_MANS)

dvcont_SOURCES = dvcont.c
dvcont_LDADD = ../librom1394/librom1394.la ../libavc1394/libavc1394.la \
	@LIBRAW1394_LIBS@

romtest_SOURCES = romtest.c
romtest_LDADD = ../librom1394/librom1394.la \
	@LIBRAW1394_LIBS@

mkrfc2734_SOURCES = mkrfc2734.c
mkrfc2734_LDADD = ../librom1394/librom1394.la \
	@LIBRAW1394_LIBS@

setrom_SOURCES = setrom.c
setrom_LDADD = ../librom1394/librom1394.la \
	@LIBRAW1394_LIBS@

avc_vcr_SOURCES = avc_vcr.c
avc_vcr_LDADD = ../libavc1394/libavc1394.la \
	@LIBRAW1394_LIBS@

panelctl_SOURCES = panelctl.c
panelctl_LDADD = ../librom1394/librom1394.la ../libavc1394/libavc1394.la \
	@LIBRAW1394_LIBS@

INCLUDES = @LIBRAW1394_CFLAGS@

