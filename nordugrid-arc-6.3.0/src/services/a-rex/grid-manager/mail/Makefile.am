pkglibexec_PROGRAMS = smtp-send
dist_pkglibexec_SCRIPTS = smtp-send.sh
noinst_LTLIBRARIES = libmail.la

smtp_send_SOURCES = smtp-send.c
smtp_send_LDADD = $(LIBRESOLV)

libmail_la_SOURCES = send_mail.cpp send_mail.h
libmail_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS)
