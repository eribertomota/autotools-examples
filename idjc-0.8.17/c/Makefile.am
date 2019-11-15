pkglib_LTLIBRARIES = idjc.la

idjc_la_SOURCES = agc.c agc.h audio_feed.c audio_feed.h avcodecdecode.c avcodecdecode.h bsdcompat.c bsdcompat.h			\
			\
				compressor.c compressor.h dbconvert.c dbconvert.h dyn_lame.c dyn_lame.h encoder.c						\
			\
				encoder.h fade.c fade.h flacdecode.c flacdecode.h gnusource.h ialloc.c ialloc.h id3.c id3.h kvpdict.c	\
			\
				kvpdict.h kvpparse.c kvpparse.h lame.h live_mp3_encoder.c live_mp3_encoder.h live_ogg_encoder.c			\
			\
				live_ogg_encoder.h live_oggflac_encoder.c live_oggflac_encoder.h live_oggspeex_encoder.c				\
			\
				live_oggspeex_encoder.h main.c main.h mic.c mic.h mixer.c mixer.h mp3dec.c mp3dec.h mp3tagread.c		\
			\
				mp3tagread.h ogg_flac_dec.c ogg_flac_dec.h ogg_speex_dec.c ogg_speex_dec.h ogg_vorbis_dec.c				\
			\
				ogg_vorbis_dec.h oggdec.c oggdec.h peakfilter.c peakfilter.h recorder.c recorder.h sig.c sig.h			\
			\
				sndfiledecode.c sndfiledecode.h sndfileinfo.c sndfileinfo.h sourceclient.c sourceclient.h speextag.c	\
			\
				speextag.h streamer.c streamer.h xlplayer.c xlplayer.h live_mp2_encoder.c live_mp2_encoder.h			\
			\
				live_aac_encoder.c live_aac_encoder.h smoothing.c smoothing.h dyn_mpg123.c dyn_mpg123.h mpg123.h			\
			\
				ogg_opus_dec.c ogg_opus_dec.h vorbistagparse.c vorbistagparse.h live_oggopus_encoder.c					\
			\
				live_oggopus_encoder.h live_webm_encoder.c live_webm_encoder.h

idjc_la_CFLAGS = ${GLIB_CFLAGS} ${LIBAVCODEC_CFLAGS} ${LIBAVFORMAT_CFLAGS} ${LIBAVUTIL_CFLAGS} ${LIBFLAC_CFLAGS}		\
			\
				${LIBJACK_CFLAGS} ${MPG123_CFLAGS} ${LIBSAMPLERATE_CFLAGS} ${SHOUTIDJC_CFLAGS} ${LIBSNDFILE_CFLAGS} 	\
			\
				${LIBSPEEX_CFLAGS} ${LIBVORBISENC_CFLAGS} ${LIBVORBIS_CFLAGS} ${TWOLAME_CFLAGS} ${OPUS_CFLAGS}			\
			\
				${LIBSWRESAMPLE_CFLAGS} ${LIBOGG_CFLAGS} -O2 -Wall -std=gnu99
				
idjc_la_LIBADD = ${DYN_LIBS} ${GLIB_LIBS} ${LIBAVCODEC_LIBS} ${LIBAVFORMAT_LIBS} ${LIBAVUTIL_LIBS} ${LIBFLAC_LIBS} 		\
			\
				${LIBJACK_LIBS} ${MPG123_LIBS} ${LIBMP3LAME} ${LIBM} ${LIBSAMPLERATE_LIBS} ${SHOUTIDJC_LIBS}			\
			\
				${LIBSNDFILE_LIBS} ${LIBSPEEX_LIBS} ${LIBVORBISENC_LIBS} ${LIBVORBIS_LIBS} ${TWOLAME_LIBS} 				\
			\
				${LIBSWRESAMPLE_LIBS} ${OPUS_LIBS} ${LIBOGG_LIBS} -lpthread
				
idjc_la_LDFLAGS = ${DYN_LDFLAGS} -no-undefined -avoid-version -module
