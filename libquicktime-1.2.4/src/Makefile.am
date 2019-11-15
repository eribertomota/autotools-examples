localedir = $(datadir)/locale
lib_LTLIBRARIES= libquicktime.la

AM_CFLAGS = -DLOCALE_DIR=\"$(localedir)\"

#
# Library dependencies
# Maybe we need zlib to read compressed quicktime headers
#
libquicktime_la_LIBADD = @ICONV_LIBS@ @LTLIBINTL@

libquicktime_la_LDFLAGS = -export-dynamic -version-number 2

# build only the files, which can be compiled

# Different files for dynamic plugins and others

if HAVE_FSEEKO
FSEEKO_SRC =
else
FSEEKO_SRC = lqt_fseeko.c
endif

lqt_sources = lqt_codecs.c lqt_quicktime.c $(FSEEKO_SRC)

# lqt_sources = codecs.c  plugin.c quicktime.c

libquicktime_la_SOURCES= \
audio.c \
$(lqt_sources) \
atom.c \
avi_avih.c \
avi_guid.c \
avi_hdrl.c \
avi_idx1.c \
avi_info.c \
avi_indx.c \
avi_ix.c \
avi_movi.c \
avi_odml.c \
avi_riff.c \
avi_strf.c \
avi_strh.c \
avi_strl.c \
chan.c \
charset.c \
clap.c \
cmodel_default.c \
cmodel_yuv420p.c \
cmodel_yuv422.c \
colormodels.c \
colr.c \
compression.c \
ctab.c \
ctts.c \
dinf.c \
dref.c \
edts.c \
elst.c \
enda.c \
esds.c \
fiel.c \
frma.c \
ftab.c \
ftyp.c \
gama.c \
gmhd.c \
gmhd_text.c \
gmin.c \
hdlr.c \
imgp.c \
impn.c \
iods.c \
language.c \
log.c \
matrix.c \
mdat.c \
mdhd.c \
mdia.c \
minf.c \
moov.c \
mvhd.c \
multichannel.c \
navg.c \
ndhd.c \
nloc.c \
nmhd.c \
obji.c \
pano.c \
pasp.c \
pdat.c \
pHdr.c \
qtatom.c \
qtvr.c \
smhd.c \
stbl.c \
stco.c \
stsc.c \
stsd.c \
stsdtable.c \
stss.c \
stsz.c \
stts.c \
texttrack.c \
timecode.c \
tkhd.c \
trak.c \
translation.c \
tcmi.c \
tmcd.c \
tref.c \
udta.c \
useratoms.c \
util.c \
vmhd.c \
vrsc.c \
vrnp.c \
vrni.c \
wave.c \
workarounds.c \
lqt_bufalloc.c \
lqt_codecfile.c \
lqt_color.c \
lqt_codecinfo.c \
lqt_divx.c \
lqt_qtvr.c

INCLUDES = -I$(top_srcdir)/include -I$(top_builddir)/include
