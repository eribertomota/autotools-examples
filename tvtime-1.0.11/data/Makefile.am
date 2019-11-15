# data/Makefile.am distributes the shared data files tvtime needs.
# Copyright (C) 2002, 2003  Billy Biggs
#
# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 2 of the License, or (at
# your option) any later version.
#
# This program is distributed in the hope that it will be useful, but
# WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
# General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 675 Mass Ave, Cambridge, MA 02139, USA.

tvtimedatadir = $(pkgdatadir)
dist_tvtimedata_DATA = FreeMonoBold.ttf tvtimeSansBold.ttf \
	filmstrip_0000.png filmstrip_0001.png filmstrip_0002.png \
	filmstrip_0003.png filmstrip_0004.png infoicon_0000.png

EXTRA_DIST = COPYING.tvtimeSansBold COPYING.FreeMonoBold \
	tvtimeSansBold.sfd FreeMonoBold.sfd

.ttf: .pe .sfd
	pfaedit -script $^

.PHONY: uninstall-hook
uninstall-hook:
	-rmdir -p '$(DESTDIR)$(tvtimedatadir)'
