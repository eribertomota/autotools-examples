SUBDIRS=. tools tests doc

OGGDIR=built-streams
kateincdir=$(includedir)/kate
katepcdir=$(libdir)/pkgconfig

lib_LTLIBRARIES=lib/libkate.la
kateinc_HEADERS=include/kate/kate.h include/kate/kate_config.h
katepc_DATA=misc/pkgconfig/kate.pc
noinst_DATA=misc/pkgconfig/kate-uninstalled.pc

if HAVE_OGG
lib_LTLIBRARIES+=lib/liboggkate.la
kateinc_HEADERS+=include/kate/oggkate.h
katepc_DATA+=misc/pkgconfig/oggkate.pc
noinst_DATA+=misc/pkgconfig/oggkate-uninstalled.pc
endif

LIBTOOLFLAGS=--silent

AM_CPPFLAGS=-I $(top_srcdir)/src -I $(top_srcdir)/include

lib_libkate_la_SOURCES=\
  src/kate.c src/kate_info.c src/kate_comment.c src/kate_granule.c src/kate_event.c \
  src/kate_motion.c src/kate_text.c src/kate_tracker.c src/kate_fp.c src/kate_font.c \
  src/kate_encode_state.c src/kate_encode.c \
  src/kate_decode_state.c src/kate_decode.c \
  src/kate_packet.c src/kate_bitwise.c src/kate_rle.c src/kate_meta.c \
  src/kate_high.c

lib_liboggkate_la_SOURCES=\
  src/kate_ogg.c

noinst_HEADERS=\
  src/kate_internal.h \
  src/kate_encode_state.h src/kate_decode_state.h \
  src/kate_bitwise.h src/kate_fp.h src/kate_rle.h src/kate_meta.h

lib_libkate_la_CFLAGS=@CWARNFLAGS_FULL@ @CFLAGS_FORTIFY_SOURCE@ @CFLAGS_DEBUG@
lib_libkate_la_LDFLAGS=-version-info @LIBKATE_SHARED_VERSION@ -no-undefined
lib_liboggkate_la_CFLAGS=@CWARNFLAGS_FULL@ @OGG_CFLAGS@ @CFLAGS_FORTIFY_SOURCE@ @CFLAGS_DEBUG@
lib_liboggkate_la_LDFLAGS=-version-info @LIBOGGKATE_SHARED_VERSION@ -no-undefined # @OGG_LIBS@

lib_liboggkate_la_LIBADD=lib/libkate.la

am__tar = ${AMTAR} chof - --owner=0 --group=0 --exclude=CVS --exclude=.cvsignore "$$tardir"

STREAMS=@STREAMS@

if HAVE_OGG

video_theora_ogg:=$(shell ls video.theora.ogg 2> /dev/null || ls video.theora.ogv 2> /dev/null)

.PRECIOUS: $(OGGDIR)/%.kate.ogg
$(OGGDIR)/%.kate.ogg: examples/kate/%.kate tools/kateenc
	@echo " Building Kate stream from $<"
	@mkdir -p $(dir $@)
	@$(LIBTOOL) -dlopen lib/libkate.la --mode=execute ./tools/kateenc -s `echo $< | $(GENHASH) | cut -b1-8` -c x-test -l en -t kate -o $(OGGDIR)/$(notdir $<).ogg $<

$(OGGDIR)/%.ogg: $(OGGDIR)/%.kate.ogg tools/kateenc
if HAVE_OGG_MERGE
	@if test "x${video_theora_ogg}" = "x"; then \
	  echo "video.theora.ogv not found, Kate streams will not be merged with video."; \
	else \
	  echo " Merging video with Kate stream from $<"; \
	  $(OGG_MERGE) -o $@ $(video_theora_ogg) $(OGGDIR)/$(notdir $<); \
	fi
else
	echo "Building $@ needs either oggmerge or oggz-merge"
endif

streams: $(foreach stream, $(STREAMS), $(OGGDIR)/$(notdir $(basename $(stream))).ogg)

kate-streams: $(foreach stream, $(STREAMS), $(OGGDIR)/$(notdir $(basename $(stream))).kate.ogg)

else
streams:
	@echo "libogg not found, make streams needs it"

endif

.PHONY: force-doc
force-doc:
	$(MAKE) -C doc force-doc

EXTRA_DIST=\
  README INSTALL AUTHORS COPYING THANKS ChangeLog \
  misc/pkgconfig/kate.pc.in misc/pkgconfig/kate-uninstalled.pc.in \
  misc/pkgconfig/oggkate.pc.in misc/pkgconfig/oggkate-uninstalled.pc.in \
  examples \
  contrib

