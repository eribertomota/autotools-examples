
INCLUDES = $(APXS_INCLUDE) $(APR_INCLUDE) $(MYSQL_INCLUDE)

mod_musicindex_la_LDFLAGS = -shared -module \
	-avoid-version -export-symbols-regex "musicindex_module" \
	$(APXS_LIBS) $(APR_LIBS) \
	$(VORBIS_LIBS) $(VORBISFILE_LIBS) \
	$(MAD_LIBS) $(ID3TAG_LIBS) \
	$(LIBFLAC_LIBS) $(MYSQL_LIBS) \
	$(LIBINTL)

#libexec_PROGRAMS = mod_musicindex.so
lib_LTLIBRARIES = mod_musicindex.la

mod_musicindex_la_CFLAGS = -Wall -pedantic -fstrict-aliasing \
	$(APXS_CFLAGS) \
	$(APR_CFLAGS) \
	$(VORBIS_CFLAGS) \
	$(LIBFLAC_CFLAGS) \
	$(MYSQL_CFLAGS)

mod_musicindex_la_CPPFLAGS = $(APR_CPPFLAGS)

mod_musicindex_la_SOURCES = mod_musicindex.c \
	html.c \
	http.c \
	sort.c \
	config.c \
	playlist.c

if ENABLE_CODEC_VORBIS
mod_musicindex_la_SOURCES += playlist-vorbis.c
endif

if ENABLE_CODEC_FLAC
mod_musicindex_la_SOURCES += playlist-flac.c
endif

if ENABLE_CODEC_MP3
mod_musicindex_la_SOURCES += playlist-mp3.c
endif

if ENABLE_CODEC_MP4
mod_musicindex_la_SOURCES += playlist-mp4.c
endif

if ENABLE_CACHE_FILE
mod_musicindex_la_SOURCES += cache-file.c
endif

if ENABLE_CACHE_MYSQL
mod_musicindex_la_SOURCES += cache-mysql.c
endif

if ENABLE_OUTPUT_ARCHIVE
mod_musicindex_la_SOURCES += output-tarball.c
endif

noinst_HEADERS = \
	cache-mysql.h \
	cache-file.h \
	config.h \
	html.h \
	http.h \
	mod_musicindex.h \
	playlist.h \
	playlist-flac.h \
	playlist-mp3.h \
	playlist-mp4.h \
	playlist-vorbis.h \
	sort.h

install: $(lib_LTLIBRARIES)
	$(mkinstalldirs) "$(DESTDIR)$(libdir)"
if BUILD_FOR_APACHE2
	$(APXS) -S LIBEXECDIR="$(DESTDIR)$(libdir)" -i -n musicindex mod_musicindex.la
else
	$(APXS) -S LIBEXECDIR="$(DESTDIR)$(libdir)" -i -n musicindex .libs/mod_musicindex.so
endif
