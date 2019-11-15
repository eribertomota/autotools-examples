lib_LTLIBRARIES = libifp.la
libifp_la_SOURCES = prim.c comp.c readwrite.c userfile.c ifp_os_libusb.c error_strings.c tuner.c
libifp_la_LDFLAGS = -version-info 5:4:1 -no-undefined $(LIBUSB)

include_HEADERS = $(top_srcdir)/include/ifp.h

# set the include path found by configure

INCLUDES = $(all_includes) -I$(top_srcdir)/include


