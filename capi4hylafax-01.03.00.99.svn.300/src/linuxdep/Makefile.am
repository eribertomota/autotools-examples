## Process this file with automake to produce Makefile.in

AUTOMAKE_OPTIONS        = foreign
CLEANFILES              = *~ comperr
MAINTAINERCLEANFILES    = Makefile.in

INCLUDES                = -I$(srcdir)/../standard -I$(srcdir)/../capi

noinst_HEADERS          = dbgLINUX.h misc.h PrctlDmp.h SysTick.h TimerList.h
noinst_LIBRARIES        = liblinuxdep.a

liblinuxdep_a_SOURCES   = CapiBase.cpp dbgLEVEL.cpp misc.cpp PrctlDmp.cpp SecTimer.cpp SysTick.cpp TimerList.cpp
