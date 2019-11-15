#
# NASPRO - The NASPRO Architecture for Sound PROcessing
# A simple command line effect processor using LV2 plugins
#
# Copyright (C) 2011-2014 Stefano D'Angelo
#
# See the COPYING file for license conditions.
#

AM_CFLAGS = -pedantic -Wall -Werror @SNDFILE_CFLAGS@ @LILV_CFLAGS@
LIBS += @SNDFILE_LIBS@ @LILV_LIBS@

bin_PROGRAMS = lv2proc

lv2proc_SOURCES = main.c
