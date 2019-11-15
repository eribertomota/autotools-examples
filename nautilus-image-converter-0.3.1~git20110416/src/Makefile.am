AM_CPPFLAGS =						\
	-DG_LOG_DOMAIN=\"Nautilus-Image-Converter\"	\
	-DDATADIR=\"$(datadir)\"			\
	-DGNOMELOCALEDIR=\""$(datadir)/locale"\" 	\
	-I$(top_srcdir)					\
	-I$(top_builddir)				\
	$(WARN_CFLAGS)                                  \
	$(DISABLE_DEPRECATED_CFLAGS)			\
	$(NAUTILUS_CFLAGS)

nautilus_extensiondir=$(NAUTILUS_EXTENSION_DIR)

nautilus_extension_LTLIBRARIES=libnautilus-image-converter.la

libnautilus_image_converter_la_SOURCES =				\
	image-converter.c						\
	nautilus-image-converter.c	nautilus-image-converter.h	\
	nautilus-image-resizer.c	nautilus-image-resizer.h	\
	nautilus-image-rotator.c	nautilus-image-rotator.h

libnautilus_image_converter_la_LDFLAGS = -module -avoid-version
libnautilus_image_converter_la_LIBADD  = $(NAUTILUS_LIBS)
