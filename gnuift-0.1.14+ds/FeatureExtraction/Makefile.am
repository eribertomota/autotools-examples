#     -*- mode: makefile -*-

#     GIFT, a flexible content based image retrieval system.
#     Copyright (C) 1998, 1999, 2000, 2001, 2002, CUI University of Geneva

#     This program is free software; you can redistribute it and/or modify
#     it under the terms of the GNU General Public License as published by
#     the Free Software Foundation; either version 2 of the License, or
#     (at your option) any later version.

#     This program is distributed in the hope that it will be useful,
#     but WITHOUT ANY WARRANTY; without even the implied warranty of
#     MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#     GNU General Public License for more details.

#     You should have received a copy of the GNU General Public License
#     along with this program; if not, write to the Free Software
#     Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA  02111-1307  USA

# libraries

david_sources   = extract_block_features.c gabor.c rgb2hsv_utils.c quantize.c

AM_CPPFLAGS= -I$(top_srcdir)/libSquirePPM/ -I$(top_srcdir)/libSquireFFT/ -D NO_FLAT_FEATURES


gift_extract_features_SOURCES = $(david_sources) extract_features.c

gift_write_feature_descs_SOURCES= $(david_sources) write_feature_descs.c

gift_extract_features_LDADD =  -L../libSquirePPM -lSquirePPM -lm 

gift_write_feature_descs_LDADD= -L../libSquirePPM -lSquirePPM -lm 


bin_PROGRAMS = gift-extract-features gift-write-feature-descs
EXTRA_DIST= gabor.h  gabor_old.h  gift_features.h