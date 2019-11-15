docdir = $(datadir)/doc/$(PACKAGE)

doc_DATA = gigedit_quickstart.html style.css shot_whole_app.png \
	shot_default_group.png shot_new_dimension.png shot_add_sample.png \
	routing.png shot_amp1.png shot_amp2.png shot_filter1.png \
	shot_filter2.png shot_qsampler_edit.png shot_gigedit_hosted.png

doc_sources = gigedit_quickstart.xml general_midi_drummap.sgm \
	mc505_midi_drummap.sgm from_scratch.sgm glossary.sgm keybindings.sgm \
	libgig.sgm see_also.sgm technical.sgm live_editing.sgm

EXTRA_DIST = $(doc_DATA) $(doc_sources) routing.odg

# the docbook.xsl URL below is usually mapped to the system's local copy of
# the file (via entry in /etc/xml/catalog) and only if not found, fetched
# from the internet
gigedit_quickstart.html: $(doc_sources)
	xsltproc --output $@ \
	--stringparam html.stylesheet style.css \
	http://docbook.sourceforge.net/release/xsl/current/html/docbook.xsl \
	$(srcdir)/gigedit_quickstart.xml
