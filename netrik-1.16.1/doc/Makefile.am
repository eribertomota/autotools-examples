all-am: docs

docdir = $(datadir)/doc/$(PACKAGE)

MAINTAINERCLEANFILES = Makefile.in $(TXT_FILES) $(HTML_FILES)

docclean:
	rm -f $(TXT_FILES) $(HTML_FILES) README

IN_FILES = in/hacking-layout.in in/hacking-links.in in/hacking-load.in \
in/hacking-pager.in in/hacking.in in/index.in in/keys.in \
in/hacking-search.in in/hacking-terminal.in \
in/options.in in/syntax_error.in in/config.in in/hacking-page.in

TXT_FILES = hacking-layout.txt hacking-links.txt hacking-load.txt \
hacking-pager.txt hacking.txt index.txt keys.txt \
hacking-search.txt hacking-terminal.txt \
options.txt syntax_error.txt config.txt hacking-page.txt

HTML_FILES = hacking-layout.html hacking-links.html hacking-load.html \
hacking-pager.html hacking.html index.html keys.html \
hacking-search.html hacking-terminal.html \
options.html syntax_error.html config.html hacking-page.html

man_MANS = netrik.1 netrikrc.5
doc_DATA = $(HTML_FILES) $(TXT_FILES)
EXTRA_DIST = $(doc_DATA) $(IN_FILES) $(man_MANS)

%.txt: in/%.in
	cat $<\
	|sed -e'/^$$#/d'\
	     -e'   /^$$/{'\
	     -e'      x'\
	     -e'      /^$$/d'\
	     -e'      x'\
	     -e'   }'\
	     -e'   s/$$$$<[^>]*>$$\$$\|^$$=//g'\
	     -e'   /^[^$$]/s/^/$$/'\
	     -e'   s/^$$§/§/'\
	     -e'   s/^§$$/§ /'\
	     -e'   h'\
	|fmt -c -p$$ -w82\
	|sed 's/\$$\|^§\+//g'>$@

%.html: in/%.in
	cat $<\
	|sed -e's/^$$#//'\
	     -e't'\
	     -e'   /^§\([^§]\|$$\)/d'\
	     -e'      s/&/\&amp;/g'\
	     -e'      s/\(^.\?\|[^$$].\|.[^$$]\)</\1\&lt;/g'\
	     -e'      /^[^$$§]\|^$$[^§=]/{'\
	     -e'         x'\
	     -e'         /^$$/i\' -e'<p>'\
	     -e'         g'\
	     -e'      }'\
	     -e'      /^$$§/{'\
	     -e'         x'\
	     -e'         /^$$/i\' -e'<p><pre>'\
	     -e'         g'\
	     -e'         s/^$$§//'\
	     -e'         s/^$$/ /'\
	     -e'      }'\
	     -e'      /^$$/{'\
	     -e'         x'\
	     -e'         /^[^$$§]\|^$$[^§=]/i\' -e'</p>'\
	     -e'         /^$$§/i\' -e'</pre></p>'\
	     -e'         g'\
	     -e'      }'\
	     -e'      s/$$+/ /g'\
	     -e'      s/$$.//g'\
	     -e'      s/^§§//'\
	>$@

txtdocs: $(TXT_FILES)
htmldocs: $(HTML_FILES)
docs: htmldocs txtdocs README

README:
	ln -s ../README .
