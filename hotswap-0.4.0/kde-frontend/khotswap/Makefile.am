# this has all of the subdirectories that make will recurse into.  if
# there are none, comment this out
#SUBDIRS =

# this is the program that gets installed.  it's name is used for all
# of the other Makefile.am variables
bin_PROGRAMS = khotswap

# set the include path for X, qt and KDE
INCLUDES = $(all_includes)

# the library search path. 
khotswap_LDFLAGS = $(KDE_RPATH) $(all_libraries)

# the libraries to link against.
khotswap_LDADD   = $(LIB_KFILE)

# which sources should be compiled for khotswap
khotswap_SOURCES = device.cpp  hotswapform.cpp  khotswap.cpp

# these are the headers for your project that won't be installed
noinst_HEADERS = device.h  hotswapform.h

# let automoc handle all of the meta source files (moc)
METASOURCES = AUTO

messages: rc.cpp
	$(XGETTEXT) *.cpp -o $(podir)/khotswap.pot

# this is where the desktop file will go 
desktopdir   = $(kde_appsdir)/Utilities
desktop_DATA = khotswap.desktop
