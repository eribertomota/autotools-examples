SUBDIRS = ClosedCensusData CuspedCensusData

INCLUDES = -I../headers -I.

pkginclude_HEADERS = unix_cusped_census.h unix_file_io.h

noinst_LTLIBRARIES = libunixkit.la

libunixkit_la_SOURCES = \
  unix_UI.c \
  unix_cusped_census.c \
  unix_file_io.c

EXTRA_DIST = \
  unix_closed_census_main.c \
  unix_cusped_census_main.c \
  unix_sample_main.c \
  ReadMe
