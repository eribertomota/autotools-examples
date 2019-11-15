
bin_PROGRAMS=ed2k_hash_gui

ed2k_hash_gui_CXXFLAGS = -I.. -D_GUI
ed2k_hash_gui_CFLAGS = -I.. -D_GUI
ed2k_hash_gui_LDADD = -lfltk


ed2k_hash_gui_SOURCES = \
 ../linkedlist.c        \
 ../main.c              \
 ../md4.c               \
 ../options.c           \
 ../processfile.c       \
 gui.cpp                \
 Thread.cpp             \
 Mutex.cpp              \
 Semaphore.cpp          \
 Event.cpp              \
 JobQueue.cpp           \
 MainWindow.cpp         \
 Configuration.cpp      \
 About.cpp              \
 ui.cpp

EXTRA_DIST =     \
 About.h         \
 Configuration.h \
 Event.h         \
 JobQueue.h      \
 MainWindow.h    \
 Mutex.h         \
 Semaphore.h     \
 Thread.h
        
