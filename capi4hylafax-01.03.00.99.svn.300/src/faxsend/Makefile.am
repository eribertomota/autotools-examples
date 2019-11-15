## Process this file with automake to produce Makefile.in

AUTOMAKE_OPTIONS        = foreign
CLEANFILES              = *~ comperr
MAINTAINERCLEANFILES    = Makefile.in

INCLUDES                = -I.. -I$(srcdir)/.. -I$(srcdir)/../standard \
                          -I$(srcdir)/../capi -I$(srcdir)/../convert  \
                          -I$(srcdir)/../linuxdep

LDADD                   = ../capi/libcapi.a ../convert/libconvert.a ../linuxdep/liblinuxdep.a \
                          ../standard/libstandard.a

noinst_HEADERS          = faxsend.h

bin_PROGRAMS            = c2faxsend

c2faxsend_SOURCES       = faxsend.cpp sendmain.cpp
