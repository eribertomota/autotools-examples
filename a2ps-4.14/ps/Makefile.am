## -*- Makefile -*-
## Makefile for a2ps' postscript library directory.
##
## Copyright (c) 1995-2000 Akim Demaille, Miguel Santana
##

##
## This file is part of a2ps.
##
## This program is free software; you can redistribute it and/or modify
## it under the terms of the GNU General Public License as published by
## the Free Software Foundation; either version 3, or (at your option)
## any later version.
##
## This program is distributed in the hope that it will be useful,
## but WITHOUT ANY WARRANTY; without even the implied warranty of
## MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
## GNU General Public License for more details.
##
## You should have received a copy of the GNU General Public License
## along with this program; see the file COPYING.  If not, write to
## the Free Software Foundation, 59 Temple Place - Suite 330,
## Boston, MA 02111-1307, USA.
##

# As a new `feature' :), a2ps uses now even more directories
psdir = $(pkgdatadir)/ps

prologues = bw.pro bold.pro fixed.pro gray.pro color.pro gray2.pro \
matrix.pro diff.pro diffcolor.pro ul.pro
procsets = base.ps ehandler.ps
headers = a2ps.hdr color.hdr

ps_DATA = $(prologues) $(procsets) $(headers)

EXTRA_DIST = $(ps_DATA)
