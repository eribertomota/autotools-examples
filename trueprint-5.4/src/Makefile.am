## Makefile.am -- Process this file with automake to produce Makefile.in

INCLUDES		= -I$(top_builddir) -I$(top_srcdir)

bin_PROGRAMS		= trueprint
trueprint_SOURCES	= \
debug.c       index.c        lang_pascal.h  lang_verilog.c  output.h \
debug.h       index.h        lang_perl.c    lang_verilog.h  postscript.c \
diffs.c       input.c        lang_perl.h    language.c      postscript.h \
diffs.h       input.h        lang_pike.c    language.h      print_prompt.c \
expand_str.c  lang_c.c       lang_pike.h    main.c          print_prompt.h \
expand_str.h  lang_c.h       lang_report.c  main.h          printers_fl.c \
getopt.c      lang_cxx.c     lang_report.h  openpipe.c      printers_fl.h \
getopt.h      lang_cxx.h     lang_sh.c      openpipe.h      trueprint.h \
getopt1.c     lang_java.c    lang_sh.h      options.c       utils.c \
headers.c     lang_java.h    lang_text.c    options.h       utils.h \
headers.h     lang_pascal.c  lang_text.h    output.c

AM_CFLAGS		= -DPRINTERS_FILE=\"$(libdir)/printers\"
