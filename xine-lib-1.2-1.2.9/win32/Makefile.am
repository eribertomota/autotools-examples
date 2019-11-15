include $(top_srcdir)/misc/Makefile.common

EXTRA_DIST = \
	scripts/post_install.bat \
	scripts/ffmpeg_win32.patch \
	include/msvc/sys/time.h \
	include/msvc/config.h \
	include/msvc/inttypes.h \
	include/msvc/stdint.h \
	include/msvc/unistd.h \
	include/dlfcn.h \
	config.h \
	README \
	libdvdnav.def \
	libxine.def \
	libxinesupport.def \
	xine_plugin.def \
	xine.dsw


dist-hook:
	cp $(srcdir)/*.dsp $(distdir)
