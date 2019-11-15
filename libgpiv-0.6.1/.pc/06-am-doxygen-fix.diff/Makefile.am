AUX_DIST                = $(ac_aux_dir)/config.guess \
                        $(ac_aux_dir)/config.sub \
			$(ac_aux_dir)/install-sh \
                        $(ac_aux_dir)/ltconfig \
			$(ac_aux_dir)/ltmain.sh \
			$(ac_aux_dir)/mdate-sh \
			$(ac_aux_dir)/missing \
			$(ac_aux_dir)/mkinstalldirs

MAINTAINERCLEANFILES 	= Makefile.in \
			configure \
			aclocal.m4 \
			config-h.in \
			stamp-h.in \
			$(AUX_DIST)

sysconf_DATA		= gpiv.conf

EXTRA_DIST 		= Makefile.in gpiv.conf ChangeLog.1.gz \
			Doxyfile doxygen_footer.html doxygen_header.html \
			doxygen_stylesheet.css \
			config/ax_prog_doxygen.m4


SUBDIRS			= lib include


# adding doxygen support
include $(top_srcdir)/aminclude.am
DOC_INSTALL_DIR		= $(prefix)/share/doc/libgpiv3-doc/
MOSTLYCLEANFILES	= $(DX_CLEANFILES)

doxygen-install:
	install -d $(DOC_INSTALL_DIR)
if DX_COND_html
	install -d $(DOC_INSTALL_DIR)/html
	install -m 644 @DX_DOCDIR@/html/* $(DOC_INSTALL_DIR)/html
endif DX_COND_html
if DX_COND_chm
	install -d $(DOC_INSTALL_DIR)/chm
	install -m 644 @DX_DOCDIR@/chm/* $(DOC_INSTALL_DIR)/chm
if DX_COND_chi
	install -d $(DOC_INSTALL_DIR)/chi
	install -m 644 @DX_DOCDIR@/chi/* $(DOC_INSTALL_DIR)/chi
endif DX_COND_chi
endif DX_COND_chm
if DX_COND_man
	install -d $(DOC_INSTALL_DIR)/man
	install -m 644 @DX_DOCDIR@/man/* $(DOC_INSTALL_DIR)/man
endif DX_COND_man
if DX_COND_rtf
	install -d $(DOC_INSTALL_DIR)/rtf
	install -m 644 @DX_DOCDIR@/rtf/* $(DOC_INSTALL_DIR)/rtf
endif DX_COND_rtf
if DX_COND_xml
	install -d $(DOC_INSTALL_DIR)/xml
	install -m 644 @DX_DOCDIR@/xml/* $(DOC_INSTALL_DIR)/xml
endif DX_COND_xml
if DX_COND_ps
	install -d $(DOC_INSTALL_DIR)/ps
	install -m 644 @DX_DOCDIR@/ps/* $(DOC_INSTALL_DIR)/ps
endif DX_COND_ps
if DX_COND_pdf
	install -d $(DOC_INSTALL_DIR)/pdf
	install -m 644 @DX_DOCDIR@/pdf/* $(DOC_INSTALL_DIR)/pdf
endif DX_COND_pdf
if DX_COND_latex
	install -d $(DOC_INSTALL_DIR)/latex
	install -m 644 @DX_DOCDIR@/latex/* $(DOC_INSTALL_DIR)/latex
endif DX_COND_latex
if DX_COND_man
	install -d $(DOC_INSTALL_DIR)/man
	install -m 644 @DX_DOCDIR@/man/* $(DOC_INSTALL_DIR)/man
endif DX_COND_man

doxygen-uninstall:
	rm -rf $(DOC_INSTALL_DIR)
