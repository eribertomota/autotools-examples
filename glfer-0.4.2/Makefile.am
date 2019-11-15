bin_PROGRAMS = glfer mixer

#	jason.c		
#	jason.h		

glfer_SOURCES =	\
	glfer.c	\
	glfer.h	\
	fft_radix2.c 	\
	fft_radix2.h 	\
	fft.c 	\
	fft.h 	\
	audio.c \
	audio.h \
	avg.c	\
	avg.h	\
	cw_rx.c	\
	cw_rx.h	\
	util.c	\
	util.h	\
	qrs.c	\
	qrs.h	\
	rcfile.c	\
	rcfile.h	\
	source.c	\
	source.h	\
	wav_fmt.c	\
	wav_fmt.h	\
	mtm.c	\
	mtm.h	\
	lmp.c	\
	lmp.h	\
	bell-p-w.c	\
	bell-p-w.h	\
	g-l_dpss.c	\
	g-l_dpss.h	\
	hparma.c	\
	hparma.h	\
	g_main.c 	\
	g_main.h 	\
	g_about.c 	\
	g_about.h 	\
	g_txmsg.c	\
	g_txmsg.h	\
	g_options.c	\
	g_options.h	\
	g_scope.c	\
	g_scope.h	\
	g_file_dialogs.c\
	g_file_dialogs.h

glfer_LDADD =  @GTK_LIBS@ 
INCLUDES = @GTK_CFLAGS@

mixer_sources = mixer.c

man_MANS = glfer.1

EXTRA_DIST = HACKING TODO glfer.lsm $(man_MANS)