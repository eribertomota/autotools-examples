# -*- Mode: makefile  -*-
#
# $Id: Makefile.am,v 1.6 2003/08/20 09:45:20 prudhomm Exp $
#
# SUMMARY:      
# USAGE:        make <make-target>
#
# AUTHOR:       Christophe Prud'homme
# ORG:           
# E-MAIL:       prudhomm@users.sourceforge.net
#
# ORIG-DATE:     2-Nov-96 at 03:56:10
# LAST-MOD: 20-Aug-03 at 08:24:08 by Christophe Prud'homme
#
# DESCRIPTION:  
#
#  This file is part of Freefem.
#
#  Copyright (C) 1996-2003 Christophe Prud'homme <prudhomm@users.sourceforge.net>
#
#  Freefem is free software; you can redistribute it and/or modify
#  it under the terms of the GNU General Public License as published by
#  the Free Software Foundation; either version 2 of the License, or
#  (at your option) any later version.
# 
#  Freefem is distributed in the hope that it will be useful,
#  but WITHOUT ANY WARRANTY; without even the implied warranty of
#  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#  GNU General Public License for more details.
#  
#  You should have received a copy of the GNU General Public License
#  along with this program; if not, write to the Free Software
#  Foundation, Inc., 675 Mass Ave, Cambridge, MA 02139, USA.
#
#
#  - Look in GNU Coding standards for further informations
#
# DESCRIP-END.	

lib_LTLIBRARIES		= libfreefem.la

libfreefem_la_LDFLAGS 	= -version-info 0:0:0 -no-undefined
libfreefem_la_SOURCES	= femDisk.cpp \
			  femFunction.cpp \
			  femGibbs.cpp \
			  femGraphicDeviceIndependent.cpp \
			  femGraphicX11.cpp \
			  femIdentifier.cpp \
			  femLexical.cpp \
			  femMesh.cpp \
			  femMisc.cpp \
			  femSolver.cpp \
			  femSolver1.cpp \
			  femSolver1c.cpp \
			  femParser.cpp \
			  femTreeNode.cpp \
			  fem.cpp



include_HEADERS		= femDisk.hpp \
			  femCommon.hpp \
			  femFunction.hpp \
			  femGibbs.hpp \
			  femGraphic.hpp \
			  femGraphicDeviceIndependent.hpp \
			  femIdentifier.hpp \
			  femLexical.hpp \
			  femMesh.hpp \
			  femMisc.hpp \
			  femSolver.hpp \
			  femSolver1.hpp \
			  femSolver1c.hpp \
		  	  femParser.hpp \
			  femTreeNode.hpp


SUFFIXES		= .hpp .cpp

