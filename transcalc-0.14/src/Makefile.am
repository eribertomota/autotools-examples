bin_PROGRAMS = transcalc


PACKAGE = @PACKAGE@
VERSION = @VERSION@

transcalc_c_sources =  \
	transcalc.c \
	setup_menu.c \
	options.c \
	help.c \
	setup_body.c \
	setup_status.c \
	image_util.c \
	unitscombo.c \
	setup_label.c \
	setup_values.c \
	setup_transgui.c \
	file_io.c \
	print_trans.c \
	microstrip.c \
	c_microstrip.c \
	rectwaveguide.c \
	coax.c \
	callback_general.c \
	fnmatch.c

transcalc_h_sources =  \
	units.h \
	transcalc.h \
	setup_menu.h \
	unitscombo.h \
	menu.h \
	help.h \
	body.h \
	options.h \
	setup.h \
	file_io.h \
	microstrip.h \
	c_microstrip.h \
	rectwaveguide.h \
	coax.h \
	convert.h \
	callback_general.h \
	fnmatch.h

transcalc_SOURCES = $(transcalc_c_sources) \
        $(transcalc_h_sources)

INCLUDES = @GTK_CFLAGS@ -DDATADIR=\"@datadir@\"

LDADD = @GTK_LIBS@ 

CLEANFILES = *~
DISTCLEANFILES = .deps/*.P

#EXTRA_DIST = example1.trc 000.trc cstrip_kj_1.trc hp.trc ustrip_jansen.trc 001.trc cstrip_kj_2.trc ustrip50fr4.trc

