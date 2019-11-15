AUTOMAKE_OPTIONS = foreign
bin_PROGRAMS = bitstormlite

localedir =  $(datadir)/locale
INCLUDES = $(GTK_CFLAGS) -DLOCALEDIR=\"$(localedir)\"

bitstormlite_LDFLAGS = -lpthread $(GTK_LIBS) `curl-config --libs`
bitstormlite_LDADD = $(LIBINTL)

bitstormlite_SOURCES = bdict.cpp\
		BitSet.cpp\
		blist.cpp\
		BTTask.cpp\
		EpollReactor.cpp\
		LiteWindow.cpp\
		main.cpp\
		PeerAcceptor.cpp\
		PeerLink.cpp\
		PeerManager.cpp\
		PieceRequest.cpp\
		sha1.cpp\
		Socket.cpp\
		Storage.cpp\
		TCPTracker.cpp\
		UDPTracker.cpp\
		ThreadMutex.cpp\
		TorrentFile.cpp\
		TrackerManager.cpp\
		xmlnode.cpp\
		UPnpNat.cpp\
		NewTaskWindow.cpp\
		RateMeasure.cpp

noinst_HEADERS = bdict.h\
		bobject.h\
		log.h\
		sha1.h\
		TorrentFile.h\
		binteger.h\
		bstring.h\
		PeerAcceptor.h\
		Socket.h\
		TrackerManager.h\
		BitSet.h\
		BTTask.h\
		PeerLink.h\
		Storage.h\
		utils.h\
		BitStorm.h\
		EpollReactor.h\
		PeerManager.h\
		TCPTracker.h\
		blist.h\
		LiteWindow.h\
		PieceRequest.h\
		ThreadMutex.h\
		UDPTracker.h\
		xmlnode.h\
		UPnpNat.h\
		NewTaskWindow.h\
		RateMeasure.h\
		gettext.h

