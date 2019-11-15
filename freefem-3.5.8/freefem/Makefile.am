# -*- Mode: makefile  -*-
#
# $Id: Makefile.am,v 1.5 2001/10/08 21:54:22 prudhomm Exp $
#
# SUMMARY:      
# USAGE:        make <make-target>
#
# AUTHOR:       Christophe Prud'homme
# ORG:           
# E-MAIL:       Christophe.Prudhomme@asci.fr
#
# ORIG-DATE:     2-Nov-96 at 03:56:10
# LAST-MOD:  8-Oct-01 at 16:55:46 by Christophe Prud'homme
#
# DESCRIPTION:  
#  - Look in GNU Coding standards for further informations
#
# DESCRIP-END.	

# INCLUDES		= $(KFEM_INCLUDES) $(MICO_INCLUDES) -I$(idldir)
INCLUDES		= $(KFEM_INCLUDES) -I$(idldir)

SUBDIRS			= fem 


bin_PROGRAMS		= freefem

freefem_SOURCES		= main.cpp
freefem_LDADD		= fem/libfreefem.la

man_MANS		= freefem.1
EXTRA_DIST 		= $(man_MANS)

SUFFIXES		= .cxx .h .hpp .cpp .idl


