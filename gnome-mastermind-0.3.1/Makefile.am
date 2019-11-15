SUBDIRS = ui src themes po desktop icons help

EXTRA_DIST = config.rpath 	\
	    AUTHORS	\
	    BUGS	\
	    COPYING	\
	    copyright   \
	    copyright-artwork \
	    INSTALL	\
	    NEWS	\
	    README	\
	    TODO	\
	    autogen.sh  \
	    configure.ac\
	    intltool-extract.in\
	    intltool-merge.in\
	    intltool-update.in \
	    gnome-doc-utils.make 
	
DISTCLEANFILES = \
	         intltool-extract \
	         intltool-merge \
	         intltool-update \
		 gnome-doc-utils.make 

DISTCHECK_CONFIGURE_FLAGS = --disable-scrollkeeper

doc_DATA = TODO

ACLOCAL_AMFLAGS = -I m4

gsettings_SCHEMAS = org.autistici.gnome-mastermind.gschema.xml
EXTRA_DIST += $(gsettings_SCHEMAS)
@GSETTINGS_RULES@
