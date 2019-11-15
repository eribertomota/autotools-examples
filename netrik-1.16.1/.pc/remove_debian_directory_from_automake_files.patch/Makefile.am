SUBDIRS = doc debian

AUTOMAKE_OPTIONS = foreign

docdir = $(datadir)/doc/$(PACKAGE)

doc_DATA = README AUTHORS COPYING LICENSE TODO NEWS

bin_PROGRAMS = netrik

MAINTAINERCLEANFILES = aclocal.m4 config.h.in configure Makefile.in \
install-sh missing mkinstalldirs

netrik_SOURCES = cfg.c cfg.h cmdline.c cmdline.h debug.c \
debug.h dump-tree.c facilities.c http-parse-header.c http-parse-header.h \
http.c http.h items.c items.h layout.c layout.h links.c links.h load.c load.h \
pager.c pager.h parse-elements.c parse-struct.c parse-syntax.c pre-render.c \
render.c render.h screen.c screen.h syntax.h page.c page.h \
url.c url.h forms.c forms.h sgml.c readline.c readline.h \
search.c search.h form-file.c form-file.h \
colors.h colors.c colors-dark.c colors-bright.c \
interrupt.c interrupt.h winch.c winch.h main.c

EXTRA_DIST = LICENSE \
test/0.html test/anchors1.html test/anchors2.html test/broken.html \
test/center.html test/comments.html test/empty.html test/insdel.html \
test/links.html test/scroll.html test/sgml.html test/syntax.html \
test/table.html test/xbroken.html test/xxbroken.html test/forms.html \
test/brokenlink.html test/links2.html test/mod1.html test/mod2.html\
test/forms_post.html test/forms_post_mimeenc.html \
test/compress_gz.html.gz test/compress_bz.html.bz2 \
test/refs.html test/tags.html \
test/stat_only.http test/folding.http test/unix_eol.http test/broken.http


docs:
	cd doc && make docs

docclean:
	cd doc && make docclean
