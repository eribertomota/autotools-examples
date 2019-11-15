SUBDIRS = vst
noinst_PROGRAMS =


#######
# LV2
###
if ENABLE_LV2
lv2plugindir = @LV2DIR@/drumgizmo.lv2
lv2plugin_LTLIBRARIES = drumgizmo.la
noinst_PROGRAMS += ttlgen
lv2plugin_DATA = manifest.ttl
endif

drumgizmo_la_CXXFLAGS = -DLV2 -DLV2_PLUGIN_URI=\"http://drumgizmo.org/lv2\" \
	-fvisibility=hidden \
	$(LV2_CFLAGS) \
	$(SNDFILE_CFLAGS) \
	-I$(top_srcdir)/plugin/plugingizmo \
	-I$(top_srcdir)/plugingui \
	-I$(top_srcdir)/src \
	-I$(top_srcdir)/hugin

drumgizmo_la_CFLAGS = -fvisibility=hidden

drumgizmo_la_SOURCES = \
	$(top_srcdir)/hugin/hugin.c \
	$(top_srcdir)/plugin/plugingizmo/midievent.cc \
	$(top_srcdir)/plugin/plugingizmo/pluginlv2.cc \
	drumgizmo_plugin.cc

drumgizmo_la_LDFLAGS = -shared -module -avoid-version \
	-export-symbols drumgizmo_lv2.sym

drumgizmo_la_LIBADD = $(LV2_LIBS) \
	$(top_srcdir)/plugingui/libdggui.la \
	$(top_srcdir)/src/libdg.la

ttlgen_CPPFLAGS = $(DL_CFLAGS) -I$(top_srcdir)/plugin/plugingizmo
ttlgen_LDFLAGS = $(DL_LIBS)
ttlgen_SOURCES = \
	$(top_srcdir)/plugin/plugingizmo/ttlgen.cc

manifest.ttl : ttlgen drumgizmo.la
	./ttlgen .libs/drumgizmo.so manifest.ttl


#######
# VST
###
if ENABLE_VST
vstplugindir = $(libdir)/vst
vstplugin_LTLIBRARIES = drumgizmo_vst.la
vstplugin_DATA =
endif

drumgizmo_vst_la_CXXFLAGS = -DVST \
	-fvisibility=hidden \
	$(SNDFILE_CFLAGS) \
	-I$(top_srcdir)/plugin/plugingizmo \
	-I$(top_srcdir)/plugingui \
	-I$(top_srcdir)/src \
	-I$(top_srcdir)/hugin \
	$(VST_CPPFLAGS) -Ivst

drumgizmo_vst_la_CFLAGS = -fvisibility=hidden

drumgizmo_vst_la_SOURCES = \
	$(top_srcdir)/hugin/hugin.c \
	$(top_srcdir)/plugin/plugingizmo/midievent.cc \
	$(top_srcdir)/plugin/plugingizmo/pluginvst.cc \
	drumgizmo_plugin.cc

drumgizmo_vst_la_LDFLAGS = -shared -module -avoid-version \
	-export-symbols drumgizmo_vst.sym

drumgizmo_vst_la_LIBADD = vst/libvstsdk.la \
	$(top_srcdir)/plugingui/libdggui.la \
	$(top_srcdir)/src/libdg.la


install-data-hook:
	rm -f $(DESTDIR)/$(lv2plugindir)/drumgizmo.la
	rm -f $(DESTDIR)/$(vstplugindir)/drumgizmo_vst.la


EXTRA_DIST = \
	$(lv2plugin_DATA) \
	$(vstplugin_DATA) \
	drumgizmo_plugin.h \
	drumgizmo_lv2.sym \
	drumgizmo_vst.sym \
	$(top_srcdir)/plugin/plugingizmo/plugin.h \
	$(top_srcdir)/plugin/plugingizmo/midievent.h \
	$(top_srcdir)/plugin/plugingizmo/midnam_lv2.h \
	$(top_srcdir)/plugin/plugingizmo/pluginlv2.h \
	$(top_srcdir)/plugin/plugingizmo/pluginvst.h \
	$(top_srcdir)/plugin/plugingizmo/inline-display.h
