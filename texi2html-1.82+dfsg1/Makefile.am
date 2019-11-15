## Process this file with automake to produce Makefile.in

SUBDIRS = . doc Tests test
imagesdir = $(pkgdatadir)/images
i18ndir = $(pkgdatadir)/i18n

#
# This is to prevent texinfo.tex from being included
# in the top-level distribution directory.
TEXINFO_TEX = doc/texinfo.tex

bin_SCRIPTS = texi2html
texi2html_additional_scripts = \
	MySimple.pm \
	T2h_i18n.pm \
	texi2html.init \
	translations.pl \
	examples/l2h.init \
	T2h_l2h.pm

texi2html_sources = texi2html_configured.pl $(texi2html_additional_scripts)

noinst_SCRIPTS = manage_i18n.pl buildt2h.sh parse_8bit_makeinfo_maps.pl

EXTRA_DIST = \
	MySimple.pod \
	autogen.sh \
	$(noinst_SCRIPTS) \
	missing-texi2html \
	texi2html.pl \
	texi2html.spec \
	texi2html.spec.in \
	texi2html.pl \
	$(texi2html_additional_scripts)

dist_pkgdata_DATA = examples/l2h.init \
	examples/makeinfo.init \
	examples/xhtml.init \
	examples/html32.init \
	examples/book.init \
	examples/noheaders.init \
	examples/inlinestyle.init \
	examples/utf8.init \
	examples/enable_encoding.init \
	examples/chm.init \
	examples/roff.init \
	examples/xml.init \
	examples/mediawiki.init \
	examples/docbook.init \
	examples/tex4ht.init \
	examples/my-bib-macros.texi \
	examples/bib-example.texi \
	examples/glossary.texi 

i18n_files = i18n/de \
	i18n/es \
	i18n/fr \
	i18n/nl \
	i18n/no \
	i18n/pt \
	i18n/pt_BR \
	i18n/ja

dist_i18n_DATA = i18n/en \
	$(i18n_files)

dist_images_DATA = images/a_begin.png \
	images/a_begin_na.png \
	images/a_document.png \
	images/a_document_na.png \
	images/a_empty.png \
	images/a_end.png \
	images/a_end_na.png \
	images/a_help.png \
	images/a_help_na.png \
	images/a_index.png \
	images/a_index_na.png \
	images/a_leftdouble.png \
	images/a_leftdouble_na.png \
	images/a_left.png \
	images/a_left_na.png \
	images/a_page.png \
	images/a_page_na.png \
	images/a_rightdouble.png \
	images/a_rightdouble_na.png \
	images/a_right.png \
	images/a_right_na.png \
	images/a_searchdoc.png \
	images/a_searchdoc_na.png \
	images/a_search.png \
	images/a_search_na.png \
	images/a_tableofcon.png \
	images/a_tableofcon_na.png \
	images/a_top.png \
	images/a_top_na.png \
	images/a_up.png \
	images/a_up_na.png \
	images/bg.jpg \
	images/bg_left.png \
	images/bg_right.png \
	images/blue_dir.png \
	images/blue_down.png \
	images/blue_grab.png \
	images/blue_help.png \
	images/blue_next.png \
	images/blue_nnext.png \
	images/blue_pprev.png \
	images/blue_prev.png \
	images/blue_readme.png \
	images/blue_top.png \
	images/blue_up.png \
	images/blue_uup.png \
	images/contents_motif.png \
	images/COPYING \
	images/COPYING.Attribution-ShareAlike \
	images/GPL \
	images/README \
	images/index_motif.png \
	images/Mybg.png \
	images/next_motif.png \
	images/next_motif_gr.png \
	images/previous_motif.png \
	images/previous_motif_gr.png \
	images/spacer3.png \
	images/xy_contents.png \
	images/xy_foot.png \
	images/xy_next.png \
	images/xy_next_gr.png \
	images/xy_nextsection.png \
	images/xy_nextsection_gr.png \
	images/xy_previous.png \
	images/xy_previous_gr.png \
	images/xy_previoussection.png \
	images/xy_previoussection_gr.png \
	images/xy_up.png \
	images/xy_up_gr.png

#texi2html: $(texi2html_sources)
#	sed -e "/@MYSIMPLE@/r $(srcdir)/MySimple.pm" \
#	    -e "/@INIT@/r $(srcdir)/texi2html.init" \
#	    -e "/@T2H_TRANSLATIONS_FILE@/r $(srcdir)/translations.pl" \
#	    -e "/@T2H_L2H_INIT@/r $(srcdir)/l2h.init" \
#	    -e "/@T2H_I18N@/r $(srcdir)/T2h_i18n.pm" \
#	    -e "/@T2H_L2H@/r $(srcdir)/T2h_l2h.pm" $< >$@
#	chmod a+x $@
texi2html: $(texi2html_sources)
	$(SHELL) $(srcdir)/buildt2h.sh $@ $^ 
	chmod a+x $@

texi2html.spec: texi2html.spec.in configure
	@echo Generating $@...
	@sed -e "s/[@]PACKAGE_VERSION[@]/$(PACKAGE_VERSION)/" \
	     -e "s/[@]PACKAGE_TARNAME[@]/$(PACKAGE_TARNAME)/" $< >texi2html.tmp
	@cp texi2html.tmp texi2html.spec
	-@rm texi2html.tmp

i18n/en: texi2html.pl texi2html.init T2h_i18n.pm examples/roff.init \
                 examples/noheaders.init
	$(PERL) $(top_builddir)/manage_i18n.pl -d i18n -I . -I $(srcdir) template $^

#i18n/de i18n/nl i18n/es i18n/no i18n/pt i18n/fr: i18n/en

$(i18n_files): i18n/en
	$(PERL) $(top_builddir)/manage_i18n.pl -d i18n -I . -I $(srcdir) update

#translations.pl: i18n/de i18n/nl i18n/es i18n/no i18n/pt i18n/fr i18n/en
translations.pl: $(dist_i18n_DATA) 
	$(PERL) $(top_builddir)/manage_i18n.pl -d i18n -o $@ -I . -I $(srcdir) merge

html-local: texi2html

clean-local:
	-rm -f texi2html
