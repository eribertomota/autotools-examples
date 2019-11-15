## Process this file with automake to produce Makefile.in
SUBDIRS = src

bin_SCRIPTS = libcdaudio-config

m4datadir = $(datadir)/aclocal
m4data_DATA = libcdaudio.m4

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = libcdaudio.pc

$(pkgconfig_DATA): config.status

EXTRA_DIST = TODO libcdaudio-config.in libcdaudio.m4

