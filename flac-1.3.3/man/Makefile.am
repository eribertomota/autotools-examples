#  flac - Command-line FLAC encoder/decoder
#  Copyright (C) 2000-2009  Josh Coalson
#  Copyright (C) 2011-2016  Xiph.Org Foundation
#
#  This program is free software; you can redistribute it and/or
#  modify it under the terms of the GNU General Public License
#  as published by the Free Software Foundation; either version 2
#  of the License, or (at your option) any later version.
#
#  This program is distributed in the hope that it will be useful,
#  but WITHOUT ANY WARRANTY; without even the implied warranty of
#  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#  GNU General Public License for more details.
#
#  You should have received a copy of the GNU General Public License along
#  with this program; if not, write to the Free Software Foundation, Inc.,
#  51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA.

if FLaC__HAS_DOCBOOK_TO_MAN
flac.1: flac.sgml
	docbook-to-man $? > $@ || (docbook2man $? && mv FLAC.1 $@)

metaflac.1: metaflac.sgml
	docbook-to-man $? > $@ || (docbook2man $? && mv METAFLAC.1 $@)
else
flac.1:
	echo "*** Warning: docbook-to-man not found; man pages will not be built."
	touch $@

metaflac.1:
	touch $@
endif

man_MANS = flac.1 metaflac.1

EXTRA_DIST = $(man_MANS) flac.sgml metaflac.sgml
