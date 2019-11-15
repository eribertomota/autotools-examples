## Process this file with automake to produce Makefile.in

AUTOMAKE_OPTIONS        = foreign
CLEANFILES              = *~ comperr
MAINTAINERCLEANFILES    = Makefile.in

INCLUDES                = -I$(srcdir)/../standard

noinst_HEADERS          = c2msgdef.h    \
                          capi2def.h    \
                          CapiBase.h    \
                          CapiChan.h    \
                          CapiLay.h     \
                          CapiMsg.h     \
                          CapiStat.h    \
                          CCSFacil.h    \
                          CCSMesg.h     \
                          CCSParam.h    \
                          CCStruct.h    \
                          Channel.h     \
                          DataHand.h    \
                          DCMTrace.h    \
                          dbgCAPI.h     \
                          Facility.h    \
                          MSNList.h     \
                          PLCIList.h

noinst_LIBRARIES        = libcapi.a

libcapi_a_SOURCES       = CapiChan.cpp  \
                          CapiLay.cpp   \
                          CapiMsg.cpp   \
                          CapiStat.cpp  \
                          CCStruct.cpp  \
                          Channel.cpp   \
                          DataHand.cpp  \
                          DCMTrace.cpp  \
                          Facility.cpp  \
                          MSNList.cpp   \
                          PLCIList.cpp
