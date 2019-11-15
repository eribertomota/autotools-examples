## -*- Makefile -*-
##
## Makefile for a2ps' encodings directory.
##
## Copyright (c) 1988-1993 Miguel Santana
## Copyright (c) 1995-1999 Akim Demaille, Miguel Santana
## $Id: Makefile.am,v 1.1.1.1.2.1 2007/04/02 20:46:57 mhatta Exp $
##

# As a new `feature' :), a2ps uses now even more directories
encodingsdir = $(pkgdatadir)/encoding

# I don't want to hurt anybody here, this is under the pressure
# of many users.  Don't pay attention to the names.
major_encodings = ascii.edf iso1.edf
minor_encodings = \
ms-cp1250.edf hp.edf mac.edf ibm-cp437.edf ibm-cp850.edf iso2.edf	\
iso3.edf iso4.edf iso5.edf iso7.edf iso9.edf iso10.edf iso13.edf	\
iso15.edf koi8.edf ms-cp1251.edf euc-jp.edf

if EXTENSIONS
encodings_DATA = encoding.map $(major_encodings) $(minor_encodings)
else
encodings_DATA = encoding.map $(major_encodings)
endif

EXTRA_DIST = README encoding.map $(major_encodings) $(minor_encodings)
