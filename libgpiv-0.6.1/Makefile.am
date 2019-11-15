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
@DX_RULES@
#DOC_INSTALL_DIR		= $(prefix)/share/doc/libgpiv3-doc/

