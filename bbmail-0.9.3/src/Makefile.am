CPPFLAGS = @CPPFLAGS@ @SHAPE@ \
-DBBTOOL_GLOBAL=\"$(datadir)/bbtools/bbmail.rc\" \
-DBBTOOL_LOCAL=\"~/.bbtools/bbmail.rc\"
				
bin_PROGRAMS = bbmail
bbmail_SOURCES = bbmail.cpp bbmail.h \
		 main.cpp main.h \
		 baseresource.cpp baseresource.h \
		 resource.cpp resource.h \
		 spoollist.cpp spoollist.h \
		 mailboxmenu.cpp mailboxmenu.h \
		 blackboxstyle.h
bbmail_LDADD = @X_LIBS@ -lX11

