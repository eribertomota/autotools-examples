lib_LTLIBRARIES = libvomsmysql.la

libvomsmysql_la_SOURCES = mysqlwrap.cc mysqlwrap.h dbwrap.h
libvomsmysql_la_LIBADD = $(MYSQL_LIBS) -lcrypto
libvomsmysql_la_LDFLAGS = -module -avoid-version -no-undefined

AM_CPPFLAGS = $(MYSQL_CFLAGS)
