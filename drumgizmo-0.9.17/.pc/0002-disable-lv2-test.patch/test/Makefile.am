# Rules for the test code (use `make check` to execute)
SUBDIRS = dgreftest uitests

if ENABLE_TESTS

TESTS = resource enginetest paintertest configfile audiocache \
	audiocachefile audiocacheidmanager audiocacheeventhandler \
	randomtest atomictest syncedsettingstest imagecachetest \
	semaphoretest drumkitcreatortest bytesizeparsertest notifiertest \
	dgxmlparsertest domloadertest configparsertest midimapparsertest

EXTRA_DIST = \
	dgunit.h \
	drumkit_creator.h \
	lv2_test_host.h \
	scopedfile.h

if ENABLE_LV2
TESTS += lv2
endif

check_PROGRAMS = $(TESTS)

resource_CXXFLAGS = -DOUTPUT=\"resource\" $(SNDFILE_CFLAGS) \
	-I$(top_srcdir)/src \
	-I$(top_srcdir)/hugin
resource_LDFLAGS = $(SNDFILE_LIBS)
resource_SOURCES = \
	$(top_srcdir)/plugingui/resource.cc \
	$(top_srcdir)/plugingui/resource_data.cc \
	$(top_srcdir)/hugin/hugin.c \
	$(top_srcdir)/src/random.cc \
	dgtest.cc \
	drumkit_creator.cc \
	resource_test.cc

audiocache_CXXFLAGS = -DOUTPUT=\"audiocache\" \
	-I$(top_srcdir)/src \
	-I$(top_srcdir)/hugin -DDISABLE_HUGIN $(PTHREAD_CFLAGS) $(SNDFILE_CFLAGS)
audiocache_LDFLAGS = $(PTHREAD_LIBS) $(SNDFILE_LIBS)
audiocache_SOURCES = \
	$(top_srcdir)/src/audiocache.cc \
	$(top_srcdir)/src/audiocacheeventhandler.cc \
	$(top_srcdir)/src/audiocachefile.cc \
	$(top_srcdir)/src/audiocacheidmanager.cc \
	$(top_srcdir)/src/thread.cc \
	$(top_srcdir)/src/sem.cc \
	$(top_srcdir)/src/audiofile.cc \
	$(top_srcdir)/src/random.cc \
	dgtest.cc \
	drumkit_creator.cc \
	audiocachetest.cc

audiocachefile_CXXFLAGS = -DOUTPUT=\"audiocachefile\" \
	-I$(top_srcdir)/src \
	-I$(top_srcdir)/hugin -DDISABLE_HUGIN $(PTHREAD_CFLAGS) $(SNDFILE_CFLAGS)
audiocachefile_LDFLAGS = $(PTHREAD_LIBS) $(SNDFILE_LIBS)
audiocachefile_SOURCES = \
	$(top_srcdir)/src/audiocachefile.cc \
	$(top_srcdir)/src/thread.cc \
	$(top_srcdir)/src/sem.cc \
	$(top_srcdir)/src/audiofile.cc \
	$(top_srcdir)/src/random.cc \
	dgtest.cc \
	drumkit_creator.cc \
	audiocachefiletest.cc

audiocacheidmanager_CXXFLAGS = -DOUTPUT=\"audiocacheidmanager\" \
	\
	-I$(top_srcdir)/src \
	-I$(top_srcdir)/hugin -DDISABLE_HUGIN $(SNDFILE_CFLAGS)
audiocacheidmanager_LDFLAGS = $(SNDFILE_LIBS)
audiocacheidmanager_SOURCES = \
	$(top_srcdir)/src/audiocacheidmanager.cc \
	dgtest.cc \
	audiocacheidmanagertest.cc

audiocacheeventhandler_CXXFLAGS = -DOUTPUT=\"audiocacheeventhandler\" \
	\
	-I$(top_srcdir)/src \
	-I$(top_srcdir)/hugin -DDISABLE_HUGIN $(PTHREAD_CFLAGS) $(SNDFILE_CFLAGS)
audiocacheeventhandler_LDFLAGS = $(PTHREAD_LIBS) $(SNDFILE_LIBS)
audiocacheeventhandler_SOURCES = \
	$(top_srcdir)/src/audiocacheeventhandler.cc \
	$(top_srcdir)/src/audiocacheidmanager.cc \
	$(top_srcdir)/src/audiocachefile.cc \
	$(top_srcdir)/src/thread.cc \
	$(top_srcdir)/src/sem.cc \
	dgtest.cc \
	audiocacheeventhandlertest.cc

enginetest_CXXFLAGS = -DOUTPUT=\"enginetest\" \
	-I$(top_srcdir)/src \
	-I$(top_srcdir)/hugin $(PTHREAD_CFLAGS) $(SNDFILE_CFLAGS)
enginetest_LDFLAGS = $(PTHREAD_LIBS) $(SNDFILE_LIBS) \
	 $(top_srcdir)/src/libdg.la
enginetest_SOURCES = \
	$(top_srcdir)/hugin/hugin.c \
	dgtest.cc \
	drumkit_creator.cc \
	enginetest.cc

paintertest_CXXFLAGS = -DOUTPUT=\"paintertest\" \
	-I$(top_srcdir)/src -I$(top_srcdir)/plugingui \
	-I$(top_srcdir)/hugin $(PTHREAD_CFLAGS)
paintertest_LDFLAGS = $(top_srcdir)/plugingui/libdggui.la
paintertest_SOURCES = \
	$(top_srcdir)/hugin/hugin.c \
	dgtest.cc \
	paintertest.cc

lv2_CXXFLAGS = -DOUTPUT=\"lv2\" \
	-I$(top_srcdir)/src \
	 `pkg-config --cflags serd-0` `pkg-config --cflags lilv-0` \
	-DLV2_PATH=\"@LV2DIR@\" $(SNDFILE_CFLAGS)
lv2_LDFLAGS = `pkg-config --libs serd-0` \
	`pkg-config --libs lilv-0` -lcrypto \
	$(SNDFILE_LIBS)
lv2_SOURCES = \
	$(top_srcdir)/src/random.cc \
	dgtest.cc \
	drumkit_creator.cc \
	lv2_test_host.cc \
	lv2.cc

configfile_CXXFLAGS = -DOUTPUT=\"configfile\" \
	-I$(top_srcdir)/hugin
configfile_LDFLAGS =
configfile_SOURCES = \
	$(top_srcdir)/src/configfile.cc \
	$(top_srcdir)/hugin/hugin.c \
	dgtest.cc \
	configtest.cc

randomtest_CXXFLAGS = -DOUTPUT=\"randomtest\" \
	-I$(top_srcdir)/src \
	-I$(top_srcdir)/hugin -DDISABLE_HUGIN
randomtest_CFLAGS = -DDISABLE_HUGIN
randomtest_LDFLAGS =
randomtest_SOURCES = \
	$(top_srcdir)/src/random.cc \
	dgtest.cc \
	randomtest.cc

atomictest_CXXFLAGS = -DOUTPUT=\"atomictest\" \
	-I$(top_srcdir)/src -I$(top_srcdir)/hugin
atomictest_LDFLAGS =
atomictest_SOURCES = atomictest.cc dgtest.cc

syncedsettingstest_CXXFLAGS = -DOUTPUT=\"syncedsettingstest\" \
	-I$(top_srcdir)/src -I$(top_srcdir)/hugin
syncedsettingstest_LDFLAGS =
syncedsettingstest_SOURCES = syncedsettings.cc dgtest.cc

imagecachetest_CXXFLAGS = -DOUTPUT=\"imagecachetest\" \
	-I$(top_srcdir)/src -I$(top_srcdir)/plugingui  -I$(top_srcdir)/hugin
imagecachetest_LDFLAGS = $(top_srcdir)/plugingui/libdggui.la
imagecachetest_SOURCES = \
	$(top_srcdir)/hugin/hugin.c \
	imagecachetest.cc \
	dgtest.cc

semaphoretest_CXXFLAGS = -DOUTPUT=\"semaphoretest\" \
	-I$(top_srcdir)/src -I$(top_srcdir)/hugin $(PTHREAD_CFLAGS)
semaphoretest_LDFLAGS = $(PTHREAD_LIBS)
semaphoretest_SOURCES = \
	$(top_srcdir)/hugin/hugin.c \
	$(top_srcdir)/src/sem.cc \
	semaphoretest.cc \
	dgtest.cc

drumkitcreatortest_CXXFLAGS = -DOUTPUT=\"drumkitcreatortest\" \
	-I$(top_srcdir)/src \
	-I$(top_srcdir)/hugin -DDISABLE_HUGIN $(SNDFILE_CFLAGS)
drumkitcreatortest_CFLAGS = -DDISABLE_HUGIN
drumkitcreatortest_LDFLAGS = $(SNDFILE_LIBS)
drumkitcreatortest_SOURCES = \
	$(top_srcdir)/src/random.cc \
	dgtest.cc \
	drumkit_creator.cc \
	drumkitcreatortest.cc

bytesizeparsertest_CXXFLAGS = -DOUTPUT=\"bytesizeparsertest\" \
	-I$(top_srcdir)/src
bytesizeparsertest_LDFLAGS =
bytesizeparsertest_SOURCES = \
	$(top_srcdir)/src/bytesizeparser.cc \
	bytesizeparsertest.cc \
	dgtest.cc

notifiertest_CXXFLAGS = -DOUTPUT=\"notifiertest\" \
	-I$(top_srcdir)/src
notifiertest_LDFLAGS =
notifiertest_SOURCES = \
	notifiertest.cc \
	dgtest.cc

dgxmlparsertest_CXXFLAGS = -DOUTPUT=\"dgxmlparsertest\" \
	-I$(top_srcdir)/src -I$(top_srcdir)/hugin \
	-I$(top_srcdir)/pugixml/src
dgxmlparsertest_LDFLAGS =
dgxmlparsertest_SOURCES = \
	$(top_srcdir)/hugin/hugin.c \
	$(top_srcdir)/src/dgxmlparser.cc \
	$(top_srcdir)/pugixml/src/pugixml.cpp \
	dgxmlparsertest.cc \
	scopedfile.cc \
	dgtest.cc

domloadertest_CXXFLAGS = -DOUTPUT=\"domloadertest\" \
	-I$(top_srcdir)/src
domloadertest_LDFLAGS = \
	 $(top_srcdir)/src/libdg.la
domloadertest_SOURCES = \
	$(top_srcdir)/hugin/hugin.c \
	domloadertest.cc \
	scopedfile.cc \
	dgtest.cc

configparsertest_CXXFLAGS = -DOUTPUT=\"configparsertest\" \
	-I$(top_srcdir)/src -I$(top_srcdir)/hugin \
	-I$(top_srcdir)/pugixml/src
configparsertest_LDFLAGS =
configparsertest_SOURCES = \
	$(top_srcdir)/hugin/hugin.c \
	$(top_srcdir)/src/configparser.cc \
	$(top_srcdir)/pugixml/src/pugixml.cpp \
	configparsertest.cc \
	dgtest.cc

midimapparsertest_CXXFLAGS = -DOUTPUT=\"midimapparsertest\" \
	-I$(top_srcdir)/src -I$(top_srcdir)/hugin \
	-I$(top_srcdir)/pugixml/src
midimapparsertest_LDFLAGS =
midimapparsertest_SOURCES = \
	$(top_srcdir)/hugin/hugin.c \
	$(top_srcdir)/src/midimapparser.cc \
	$(top_srcdir)/pugixml/src/pugixml.cpp \
	scopedfile.cc \
	midimapparsertest.cc \
	dgtest.cc

endif
