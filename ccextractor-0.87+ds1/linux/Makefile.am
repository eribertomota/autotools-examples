AUTOMAKE_OPTIONS = foreign


bin_PROGRAMS = ccextractor
ccextractor_SOURCES = \
				../src/ccextractor.c \
				../src/ccextractor.h \
				../src/gpacmp4/avc_ext.c \
				../src/gpacmp4/avilib.c \
				../src/gpacmp4/av_parsers.c \
				../src/gpacmp4/base_encoding.c \
				../src/gpacmp4/bitstream.c \
				../src/gpacmp4/box_code_3gpp.c \
				../src/gpacmp4/box_code_adobe.c \
				../src/gpacmp4/box_code_apple.c \
				../src/gpacmp4/box_code_base.c \
				../src/gpacmp4/box_code_drm.c \
				../src/gpacmp4/box_dump.c \
				../src/gpacmp4/box_code_meta.c \
				../src/gpacmp4/box_funcs.c \
				../src/gpacmp4/color.c \
				../src/gpacmp4/configfile.c \
				../src/gpacmp4/data_map.c \
				../src/gpacmp4/desc_private.c \
				../src/gpacmp4/descriptors.c \
				../src/gpacmp4/drm_sample.c \
				../src/gpacmp4/error.c \
				../src/gpacmp4/gpac_ogg.c \
				../src/gpacmp4/hint_track.c \
				../src/gpacmp4/hinting.c \
				../src/gpacmp4/ipmpx_code.c \
				../src/gpacmp4/ipmpx_parse.c \
				../src/gpacmp4/isom_intern.c \
				../src/gpacmp4/isom_read.c \
				../src/gpacmp4/isom_store.c \
				../src/gpacmp4/isom_write.c \
				../src/gpacmp4/list.c \
				../src/gpacmp4/math.c \
				../src/gpacmp4/media.c \
				../src/gpacmp4/media_odf.c \
				../src/gpacmp4/meta.c \
				../src/gpacmp4/movie_fragments.c \
				../src/gpacmp4/mp4.c \
				../src/gpacmp4/odf_code.c \
				../src/gpacmp4/odf_codec.c \
				../src/gpacmp4/odf_command.c \
				../src/gpacmp4/os_config_init.c \
				../src/gpacmp4/os_divers.c \
				../src/gpacmp4/os_file.c \
				../src/gpacmp4/qos.c \
				../src/gpacmp4/sample_descs.c \
				../src/gpacmp4/slc.c \
				../src/gpacmp4/stbl_read.c \
				../src/gpacmp4/stbl_write.c \
				../src/gpacmp4/track.c \
				../src/gpacmp4/tx3g.c \
				../src/gpacmp4/url.c \
				../src/gpacmp4/utf.c \
				../src/gpacmp4/gpac/avparse.h \
				../src/gpacmp4/gpac/base_coding.h \
				../src/gpacmp4/gpac/bitstream.h \
				../src/gpacmp4/gpac/color.h \
				../src/gpacmp4/gpac/config_file.h \
				../src/gpacmp4/gpac/configuration.h \
				../src/gpacmp4/gpac/constants.h \
				../src/gpacmp4/gpac/events_constants.h \
				../src/gpacmp4/gpac/ietf.h \
				../src/gpacmp4/gpac/isomedia.h \
				../src/gpacmp4/gpac/list.h \
				../src/gpacmp4/gpac/maths.h \
				../src/gpacmp4/gpac/media_tools.h \
				../src/gpacmp4/gpac/mpeg4_odf.h \
				../src/gpacmp4/gpac/network.h \
				../src/gpacmp4/gpac/revision.h \
				../src/gpacmp4/gpac/setup.h \
				../src/gpacmp4/gpac/tools.h \
				../src/gpacmp4/gpac/utf.h \
				../src/gpacmp4/gpac/version.h \
				../src/gpacmp4/gpac/internal/avilib.h \
				../src/gpacmp4/gpac/internal/isomedia_dev.h \
				../src/gpacmp4/gpac/internal/media_dev.h \
				../src/gpacmp4/gpac/internal/odf_dev.h \
				../src/gpacmp4/gpac/internal/odf_parse_common.h \
				../src/gpacmp4/gpac/internal/ogg.h \
				../src/lib_ccx/ccx_common_common.h \
				../src/lib_ccx/ccx_common_option.h \
				../src/lib_ccx/utility.h \
				../src/lib_ccx/activity.h \
				../src/lib_ccx/asf_constants.h \
				../src/lib_ccx/avc_functions.h \
				../src/lib_ccx/bitstream.h \
				../src/lib_ccx/ccx_common_option.c \
				../src/lib_ccx/ccx_common_common.c \
				../src/lib_ccx/utility.c \
				../src/lib_ccx/activity.c \
				../src/lib_ccx/asf_functions.c \
				../src/lib_ccx/avc_functions.c \
				../src/lib_ccx/cc_bitstream.c \
				../src/lib_ccx/ccx_common_char_encoding.c \
				../src/lib_ccx/ccx_common_char_encoding.h \
				../src/lib_ccx/ccx_common_constants.c \
				../src/lib_ccx/ccx_common_constants.h \
				../src/lib_ccx/ccx_common_platform.h \
				../src/lib_ccx/ccx_common_structs.h \
				../src/lib_ccx/ccx_common_timing.c \
				../src/lib_ccx/ccx_common_timing.h \
				../src/lib_ccx/ccx_decoders_608.c \
				../src/lib_ccx/ccx_decoders_608.h \
				../src/lib_ccx/ccx_decoders_708.c \
				../src/lib_ccx/ccx_decoders_708_encoding.c \
				../src/lib_ccx/ccx_decoders_708_encoding.h \
				../src/lib_ccx/ccx_decoders_708.h \
				../src/lib_ccx/ccx_decoders_708_output.c \
				../src/lib_ccx/ccx_decoders_708_output.h \
				../src/lib_ccx/ccx_decoders_common.c \
				../src/lib_ccx/ccx_decoders_common.h \
				../src/lib_ccx/ccx_decoders_isdb.c \
				../src/lib_ccx/ccx_decoders_isdb.h \
				../src/lib_ccx/ccx_decoders_structs.h \
				../src/lib_ccx/ccx_decoders_vbi.c \
				../src/lib_ccx/ccx_decoders_vbi.h \
				../src/lib_ccx/ccx_decoders_xds.c \
				../src/lib_ccx/ccx_decoders_xds.h \
				../src/lib_ccx/ccx_demuxer.c \
				../src/lib_ccx/ccx_demuxer.h \
				../src/lib_ccx/ccx_demuxer_mxf.c \
				../src/lib_ccx/ccx_demuxer_mxf.h \
				../src/lib_ccx/ccx_dtvcc.c \
				../src/lib_ccx/ccx_dtvcc.h \
				../src/lib_ccx/ccx_encoders_common.c \
				../src/lib_ccx/ccx_encoders_common.h \
				../src/lib_ccx/ccx_encoders_curl.c \
				../src/lib_ccx/ccx_encoders_g608.c \
				../src/lib_ccx/ccx_encoders_helpers.c \
				../src/lib_ccx/ccx_encoders_helpers.h \
				../src/lib_ccx/ccx_encoders_python.c \
				../src/lib_ccx/ccx_encoders_sami.c \
				../src/lib_ccx/ccx_encoders_smptett.c \
				../src/lib_ccx/ccx_encoders_splitbysentence.c \
				../src/lib_ccx/ccx_encoders_spupng.c \
				../src/lib_ccx/ccx_encoders_srt.c \
				../src/lib_ccx/ccx_encoders_ssa.c \
				../src/lib_ccx/ccx_encoders_structs.h \
				../src/lib_ccx/ccx_encoders_transcript.c \
				../src/lib_ccx/ccx_encoders_webvtt.c \
				../src/lib_ccx/ccx_encoders_xds.c \
				../src/lib_ccx/ccx_encoders_xds.h \
				../src/lib_ccx/ccx_gxf.c \
				../src/lib_ccx/ccx_gxf.h \
				../src/lib_ccx/ccx_mp4.h \
				../src/lib_ccx/ccx_share.c \
				../src/lib_ccx/ccx_share.h \
				../src/lib_ccx/ccx_sub_entry_message.pb-c.c \
				../src/lib_ccx/ccx_sub_entry_message.pb-c.h \
				../src/lib_ccx/compile_info.h \
				../src/lib_ccx/compile_info_real.h \
				../src/lib_ccx/configuration.c \
				../src/lib_ccx/configuration.h \
				../src/lib_ccx/disable_warnings.h \
				../src/lib_ccx/dvb_subtitle_decoder.c \
				../src/lib_ccx/dvb_subtitle_decoder.h \
				../src/lib_ccx/dvd_subtitle_decoder.c \
				../src/lib_ccx/dvd_subtitle_decoder.h \
				../src/lib_ccx/es_functions.c \
				../src/lib_ccx/es_userdata.c \
				../src/lib_ccx/ffmpeg_intgr.c \
				../src/lib_ccx/ffmpeg_intgr.h \
				../src/lib_ccx/file_buffer.h \
				../src/lib_ccx/file_functions.c \
				../src/lib_ccx/general_loop.c \
				../src/lib_ccx/hamming.h \
				../src/lib_ccx/hardsubx.c \
				../src/lib_ccx/hardsubx_classifier.c \
				../src/lib_ccx/hardsubx_decoder.c \
				../src/lib_ccx/hardsubx.h \
				../src/lib_ccx/hardsubx_imgops.c \
				../src/lib_ccx/hardsubx_utility.c \
				../src/lib_ccx/lib_ccx.c \
				../src/lib_ccx/lib_ccx.h \
				../src/lib_ccx/list.h \
				../src/lib_ccx/matroska.c \
				../src/lib_ccx/matroska.h \
				../src/lib_ccx/myth.c \
				../src/lib_ccx/networking.c \
				../src/lib_ccx/networking.h \
				../src/lib_ccx/ocr.c \
				../src/lib_ccx/ocr.h \
				../src/lib_ccx/output.c \
				../src/lib_ccx/params.c \
				../src/lib_ccx/params_dump.c \
				../src/lib_ccx/sequencing.c \
				../src/lib_ccx/stdintmsc.h \
				../src/lib_ccx/stream_functions.c \
				../src/lib_ccx/teletext.h \
				../src/lib_ccx/telxcc.c \
				../src/lib_ccx/ts_functions.c \
				../src/lib_ccx/ts_functions.h \
				../src/lib_ccx/ts_info.c \
				../src/lib_ccx/ts_tables.c \
				../src/lib_ccx/ts_tables_epg.c \
				../src/lib_ccx/wtv_constants.h \
				../src/lib_ccx/wtv_functions.c \
				../src/lib_hash/sha2.c \
				../src/lib_hash/sha2.h \
				../src/protobuf-c/protobuf-c.c \
				../src/protobuf-c/protobuf-c.h \
				../src/zvbi/bcd.h \
				../src/zvbi/bit_slicer.c \
				../src/zvbi/bit_slicer.h \
				../src/zvbi/decoder.c \
				../src/zvbi/macros.h \
				../src/zvbi/misc.h \
				../src/zvbi/raw_decoder.c \
				../src/zvbi/raw_decoder.h \
				../src/zvbi/sampling_par.c \
				../src/zvbi/sampling_par.h \
				../src/zvbi/sliced.h \
				../src/zvbi/zvbi_decoder.h \
				../src/wrappers/wrapper.c \
				../src/wrappers/wrapper.h

ccextractor_CFLAGS = -std=gnu99 -Wno-write-strings -D_FILE_OFFSET_BITS=64 -DVERSION_FILE_PRESENT -DGPAC_DISABLE_VTT -DGPAC_DISABLE_OD_DUMP

ccextractor_CPPFLAGS =-I../src/lib_ccx/ -I../src/gpacmp4/ -I../src/zvbi/ -I../src/lib_hash/ -I../src/protobuf-c/ -I../src/ -I/usr/include/freetype2


ccextractor_LDADD=-lm -lpng -lz -lutf8proc -lfreetype

if SYS_IS_LINUX
ccextractor_CFLAGS += -O3 -DGPAC_CONFIG_LINUX
endif

if SYS_IS_MAC
ccextractor_CFLAGS += -DPAC_CONFIG_DARWIN -Dfopen64=fopen -Dopen64=open -Dlseek64=lseek
ccextractor_LDADD += -liconv -lz 
endif

if HARDSUBX_IS_ENABLED
ccextractor_CFLAGS += -DENABLE_HARDSUBX
ccextractor_CPPFLAGS+= ${libavcodec_CFLAGS}
ccextractor_CPPFLAGS+= ${libavformat_CFLAGS}
ccextractor_CPPFLAGS+= ${libavutil_CFALGS}
ccextractor_CPPFLAGS+= ${libswscale_CFLAGS}
AV_LIB = ${libavcodec_LIBS}
AV_LIB += ${libavformat_LIBS}
AV_LIB += ${libavutil_LIBS}
AV_LIB += ${libswscale_LIBS}
ccextractor_LDADD += $(AV_LIB)
endif

if OCR_IS_ENABLED
ccextractor_CFLAGS += -DENABLE_OCR -DPN3G_NO_CONFIG_H
LEPT_LIB = ${lept_LIBS}
LEPT_CPPFLAG = ${lept_CFLAGS}

if TESSERACT_PRESENT
TESS_LIB = ${tesseract_LIBS}
TESS_CPPFLAG = ${tesseract_CFLAGS} -I/usr/include/tesseract
else

#fix for raspberry pi not having a pkgconfig file for tesseract

if TESSERACT_PRESENT_RPI
TESS_LIB = -ltesseract
TESS_CPPFLAG = -I/usr/include/tesseract
endif
endif

ccextractor_CPPFLAGS  += $(TESS_CPPFLAG)
ccextractor_CPPFLAGS  += $(LEPT_CPPFLAG)
ccextractor_LDADD += $(TESS_LIB)
ccextractor_LDADD += $(LEPT_LIB)
endif

EXTRA_DIST = ../src/gpacmp4/gpac/sync_layer.h ../src/lib_ccx/ccfont2.xbm fonts/ icon/

#For GUI
if BUILD_WITH_GUI
bin_PROGRAMS += ccextractorGUI

ccextractorGUI_SOURCES = \
				../src/GUI/ccextractorGUI.c \
				../src/GUI/ccextractorGUI.h \
				../src/GUI/activity.c \
				../src/GUI/activity.h \
				../src/GUI/terminal.c \
				../src/GUI/preview.c \
				../src/GUI/preview.h \
				../src/GUI/ccx_cli_thread.c \
				../src/GUI/ccx_cli_thread.h \
				../src/GUI/command_builder.c \
				../src/GUI/command_builder.h \
				../src/GUI/save_load_data.c \
				../src/GUI/save_load_data.h \
				../src/GUI/file_browser.c \
				../src/GUI/file_browser.h \
				../src/GUI/popups.c \
				../src/GUI/popups.h \
				../src/GUI/tabs.c \
				../src/GUI/tabs.h \
				../src/GUI/stb_image.h \
				../src/GUI/nuklear_lib/nuklear.h \
				../src/GUI/nuklear_lib/nuklear_glfw_gl2.h

ccextractorGUI_CFLAGS = -std=gnu99


ccextractorGUI_LDADD = ${glfw3_LIBS}


if SYS_IS_LINUX
ccextractorGUI_CFLAGS += -O3 -DUNIX
ccextractorGUI_CFLAGS += ${glew_CFLAGS}
ccextractorGUI_LDADD += ${glew_LIBS}
ccextractorGUI_LDADD += -lX11 -lXinerama -lXcursor -lXi -lXrandr -lXxf86vm -lm -ldl -lpthread
endif

if SYS_IS_MAC
ccextractorGUI_CFLAGS += -O3 -DUNIX
ccextractorGUI_CFLAGS += ${glew_CFLAGS}
ccextractorGUI_LDADD += ${glew_LIBS}
ccextractorGUI_LDFLAGS = -framework OpenGL -framework Cocoa -framework IOKit -framework CoreVideo
ccextractorGUI_LDADD += -lglfw  -lm -L/usr/local/lib -lpthread
endif

if HARDSUBX_IS_ENABLED
if OCR_IS_ENABLED
ccextractorGUI_CFLAGS += -DENABLE_OCR 
endif
endif

EXTRA_DIST += ../icon/ ../fonts/

endif

