htmldir = $(docdir)/fr
htmlfiles = download.xml    \
            index.xml       \
            manual.xml      \
            plugins.xml     \
            plugins-doc.xml \
            profiles.xml    \
            reference.xml
html_DATA = $(htmlfiles:.xml=.html)

.xml.html:
	$(XSLTPROC_PROG) --nonet --xinclude -o $@ $(top_srcdir)/docs/tutorial/data/html.xsl $<

pngdir = $(docdir)/fr/shots
png_DATA = shots/ogmrip-audio-options.png         \
           shots/ogmrip-audio-options-small.png   \
           shots/ogmrip-crop.png                  \
           shots/ogmrip-crop-small.png            \
	   shots/ogmrip-encoding-queue.png        \
	   shots/ogmrip-encoding-queue-small.png  \
           shots/ogmrip-load.png                  \
           shots/ogmrip-load-small.png            \
           shots/ogmrip-main.png                  \
           shots/ogmrip-main-small.png            \
           shots/ogmrip-options.png               \
           shots/ogmrip-options-small.png         \
           shots/ogmrip-pref-advanced.png         \
           shots/ogmrip-pref-advanced-small.png   \
           shots/ogmrip-pref-general.png          \
           shots/ogmrip-pref-general-small.png    \
           shots/ogmrip-profile-audio.png         \
           shots/ogmrip-profile-audio-small.png   \
           shots/ogmrip-profile-general.png       \
           shots/ogmrip-profile-general-small.png \
           shots/ogmrip-profiles.png              \
           shots/ogmrip-profiles-small.png        \
           shots/ogmrip-profile-subp.png          \
           shots/ogmrip-profile-subp-small.png    \
           shots/ogmrip-profile-video.png         \
           shots/ogmrip-profile-video-small.png   \
           shots/ogmrip-progress.png              \
           shots/ogmrip-progress-small.png        \
           shots/ogmrip-subp-options.png          \
           shots/ogmrip-subp-options-small.png

EXTRA_DIST = $(htmlfiles) \
             sidebar.xml  \
             $(png_DATA)

CLEANFILES = $(html_DATA)

